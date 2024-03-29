### 一、滑动冲突情景分析
Android开发中，控件、容器的嵌套时常会导致滑动冲突的问题出现。下面列举常见的一种情况：
主界面一个ViewPager，包含多个fragment，fragment布局中还有可能包含HorizontalScrollView。当HorizontalScrollView向左或向右滑动时，滑动的是当前fragment布局中的控件，这没问题。但当HorizontalScrollView滑到边界时，再向前滑动的事件应该要切换到ViewPager上的fragment之间切换才对。而由于滑动冲突，HorizontalScrollView 滑到边界时，再向前滑动的触摸事件没有交给它的父控件ViewPager处理，所以，无法流畅地在fragment间切换。

### 二、滑动冲突问题处理
为了解决上面的问题，就要通过getParent().requestDisallowInterceptTouchEvent(false); 来进行事件的切换才行。源码如下：

package com.wei.wanandroid.widgets;

import android.content.Context;
import android.os.Build;
import android.support.annotation.RequiresApi;
import android.util.AttributeSet;
import android.util.Log;
import android.view.MotionEvent;
import android.widget.HorizontalScrollView;

/**
 * 解决与viewpager的滑动冲突问题
 *
 * @author: WEI
 * @date: 2018/6/25
 */
public class CusHorizontalScrollView extends HorizontalScrollView {
    private final static String TAG = "CusHorizontalScrollView";

    public CusHorizontalScrollView(Context context) {
        super(context);
    }

    public CusHorizontalScrollView(Context context, AttributeSet attrs) {
        super(context, attrs);
    }

    public CusHorizontalScrollView(Context context, AttributeSet attrs, int defStyleAttr) {
        super(context, attrs, defStyleAttr);
    }

    @RequiresApi(api = Build.VERSION_CODES.LOLLIPOP)
    public CusHorizontalScrollView(Context context, AttributeSet attrs, int defStyleAttr, int defStyleRes) {
        super(context, attrs, defStyleAttr, defStyleRes);
    }

    @Override
    public boolean onInterceptTouchEvent(MotionEvent ev) {
        return super.onInterceptTouchEvent(ev);
    }

    /**
     * 可以在此处理冲突
     * @param ev
     * @return
     */
    @Override
    public boolean dispatchTouchEvent(MotionEvent ev) {
        // 还没滑到右边，请求父控件不要拦截我的事件，事件自己处理 true ；已经滑到右边，则事件交由父控件处理 false。
//        getParent().requestDisallowInterceptTouchEvent(!isScrollToRight());
        return super.dispatchTouchEvent(ev);
    }

    /**
     * 也可以在此处理冲突
     * @param ev
     * @return
     */
    @Override
    public boolean onTouchEvent(MotionEvent ev)
    {
        switch (ev.getAction()) {
            case MotionEvent.ACTION_DOWN:
                break;

            case MotionEvent.ACTION_MOVE:
                if (isScrollToLeft() || isScrollToRight())
                {
                    Log.e(TAG, "滑到" + ( isScrollToLeft() ? "左边" : "右边" ) );
                    // 把事件交给父控件处理，例如：viewpager滑动
                    getParent().requestDisallowInterceptTouchEvent(false);
                }
                break;

            case MotionEvent.ACTION_UP:
            case MotionEvent.ACTION_CANCEL:
                // 请求父控件可以拦截事件
                getParent().requestDisallowInterceptTouchEvent(false);
                break;

            default:
        }
        return super.onTouchEvent(ev);
    }

    /**
     * 是否已经滑到了最右边
     *
     * @return
     */
    private boolean isScrollToRight() {
        return getChildAt(getChildCount() - 1).getRight() == getScrollX() + getWidth();
    }

    /**
     * 是否已经滑到了最左边
     * @return
     */
    private boolean isScrollToLeft() {
        return getScrollX() == 0;
    }
}

### 三、总结
滑动冲突的解决方式有两种：
1.外部拦截法：触摸事件都先经过父容器的拦截处理，如果父容器需要此事件就拦截，不需要就不拦截（此方法符合view事件分发机制），这样就可以解决滑动冲突问题。需要重写onInterceptTouchEvent方法，伪代码如下：

@Override
    public boolean onInterceptTouchEvent(MotionEvent ev)
    {
        boolean intercept = false;
        switch (ev.getAction()) {
            case MotionEvent.ACTION_DOWN:
              // 不能拦截，否则无法传递事件给子元素
                intercept = false;
                break;

            case MotionEvent.ACTION_MOVE:
             // 针对不同的滑动冲突，只需要修改这个条件即可，其它均不需做修改并且也不能修改
                if (滑动事件交由父容器处理)
                {
                    // 拦截事件
                    intercept = true;
                }
                else
                {
                    // 不拦截事件
                    intercept = false;
                }
                break;

            case MotionEvent.ACTION_UP:
            case MotionEvent.ACTION_CANCEL:
                // 不拦截，否则子元素可能无法接收到这两个事件
                intercept = false;
                break;

            default:
        }
        return intercept;
    }
2.内部拦截法：父容器不拦截任何事件，所有的事件都传递给子元素，如果子元素需要此事件就直接消耗掉，否则就交由父容器进行处理，这种方法和android中的事件分发机制不一致，需要配合requestDisallowInterceptTouchEvent方法才能正常工作，使用越来较外部拦截法稍显复杂。我们可以修改dispatchTouchEvent方法或者onTouchEvent方法来达到目的。伪代码如下：

@Override
    public boolean dispatchTouchEvent(MotionEvent ev) {
        switch (ev.getAction()) {
            case MotionEvent.ACTION_DOWN:
                getParent().requestDisallowInterceptTouchEvent(true);
                break;

            case MotionEvent.ACTION_MOVE:
            // 针对不同的滑动冲突，只需要修改这个条件即可，其它均不需做修改并且也不能修改
                if (父容器需要此类触摸事件)
                {
                    getParent().requestDisallowInterceptTouchEvent(false);
                }
                break;

            case MotionEvent.ACTION_UP:
            case MotionEvent.ACTION_CANCEL:
                break;

            default:
        }
        return super.dispatchTouchEvent(ev);
    }

### 源码解析
了解过事件分发的同学都知道，View事件分发的三个核心方法分别是dispatchTouchEvent、onInterceptTouchEvent、onTouchEvent。

dispatchTouchEvent主要负责事件的分发，onInterceptTouchEvent用来表示ViewGroup是否拦截事件，onTouchEvent表示当前View对事件进行处理。

我们知道，ViewGroup的onInterceptTouchEvent方法默认返回false，也就是不拦截。ViewGroup中没有重写onTouchEvent方法，它使用的是View中的onTouchEvent方法。

通过查看常用的LinearLayout、RealtiveLayout、FrameLayout的源码可以发现，它们均没有重写dispatchTouchEvent、onInterceptTouchEvent、onTouchEvent这三个方法，也就是说他们中的事件分发都是遵循ViewGroup中的规则。

HorizontalScrollView继承自FrameLayout，通过查看HorizontalScrollView的源码发现，它没有重写dispatchTouchEvent方法，而是重写了onInterceptTouchEvent和onTouchEvent方法。
