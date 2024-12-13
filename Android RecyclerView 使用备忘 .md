
### RecyclerView

GridLayoutManager item 居中：   
实际上当你指定 spanCount 的时候，item的宽度就确定了，而你要做的就是根据原item宽度来适配自己的item宽度，当然也不要想着用 layout_gravity = “center” 去相对父布局居中，毕竟RecyclerView中也不支持这个属性。
可以将item 的根布局 宽度设置为 layout_width=“match_parent” 加上 android:gravity=“center” 就OK了，
至于item之间间隔问题，使用margin就可以解决。

属性：

```
  android:overScrollMode="never"
  tools:listitem=""
  app:layoutManager="androidx.recyclerview.widget.GridLayoutManager"
  app:spanCount="4"

```

Adapter:   

```
    onCreateViewHolder(@NonNull ViewGroup parent, int viewType) {
    ItemLayoutBinding itemLayoutBinding = ItemLayoutBinding.inflate(LayoutInflater.from(parent.getContext()), parent, false);
    return new BaseViewHolder<>(itemLayoutBinding);
  }

```

前言： 由于NestedScrollView没有直接的方法让你滚动到内部RecyclerView的特定item，你需要通过计算该item在RecyclerView中的位置（即Y坐标），然后使用NestedScrollView的scrollTo()或smoothScrollTo()方法来模拟滚动。

    避免RecyclerView的item没有绘制完成，我这里使用延时滚动。获取item坐标，需要加上实际业务的padding、margin、其他布局占位等，总之根据实际情况调整。

   方法一、
   ```

   private void scrollToIndex(){
        nestedScrollView.postDelayed(new Runnable() {
            @Override
            public void run() {
                RecyclerView.LayoutManager layoutManager =recyclerView.getLayoutManager();
                if(layoutManager!=null){
                    View viewByPosition=layoutManager.findViewByPosition(index);
                    if (viewByPosition != null) {
                        int distance=viewByPosition.getTop();
                        nestedScrollView.smoothScrollTo(0, distance);//可以加上实际业务的内外间距等
                    }
                }
            }
        },1000);
    }
```
方法二、
```

private void scrollToIndex(){
        nestedScrollView.postDelayed(new Runnable() {
            @Override
            public void run() {
                RecyclerView.ViewHolder viewHolder = recyclerView.findViewHolderForAdapterPosition(index);
                if (viewHolder != null) {
                    int distance = viewHolder.itemView.getTop(); 
                    nestedScrollView.smoothScrollTo(0, distance);//可以加上实际业务的内外间距等
                }
            }
        },1000);
```
