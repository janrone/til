```
public void startFirstAnimation(View v){
//1.向后翻转
ObjectAnimator firstRotationAnim = ObjectAnimator.ofFloat(first_View, "rotationX", 0f,25f);
firstRotationAnim.setDuration(300);
//2.透明度
ObjectAnimator firstAlphaAnim = ObjectAnimator.ofFloat(first_View, "alpha", 1f,0.5f);
firstAlphaAnim.setDuration(200);
//3.缩放动画
ObjectAnimator firstScaleXAnim = ObjectAnimator.ofFloat(first_View, "scaleX", 1f,0.8f);
firstScaleXAnim.setDuration(300);
ObjectAnimator firstScaleYAnim = ObjectAnimator.ofFloat(first_View, "scaleY", 1f,0.8f);
firstScaleYAnim.setDuration(300);
//改正向旋转设置监听，执行完毕后再执行反向旋转
// firstRotationAnim.addUpdateListener(listener)
//4.向前翻转动画
ObjectAnimator firstResumeRotationAnim = ObjectAnimator.ofFloat(first_View, "rotationX",25f, 0f);
firstResumeRotationAnim.setDuration(200);
firstResumeRotationAnim.setStartDelay(200);//延迟执行
// 5.平移动画,由于缩放造成了离顶部有一段距离，需要平移上去
ObjectAnimator firstTranslationAnim = ObjectAnimator.ofFloat(first_View, "translationY",0f, -0.1f*first_View.getHeight());
firstTranslationAnim.setDuration(200);
//second_View执行平移动画--向上平移
ObjectAnimator secondeTranslationAnim = ObjectAnimator.ofFloat(second_View, "translationY",second_View.getHeight(), 0f);
secondeTranslationAnim.setDuration(200);
secondeTranslationAnim.addListener(new AnimatorListenerAdapter() {
@Override
public void onAnimationStart(Animator animation) {
super.onAnimationStart(animation);
second_View.setVisibility(View.VISIBLE);
bt.setClickable(false);
}
});
AnimatorSet set = new AnimatorSet();
set.playTogether(firstRotationAnim,firstAlphaAnim,firstScaleXAnim,firstScaleYAnim,firstResumeRotationAnim,firstTranslationAnim,secondeTranslationAnim);
set.start();
}
-----------------------------------
android 动画位移set android 属性动画上下移动
https://blog.51cto.com/u_14276/7255233

```
