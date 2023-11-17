Glide 给 View 设置背景

```
 Glide.with(this)
  .load(url)
  .into(new SimpleTarget<Drawable>() {
  @Override
  public void onResourceReady(@NonNull Drawable resource, @Nullable Transition<? super Drawable> transition) {
    view.setBackground(resource);
  }
});
```
