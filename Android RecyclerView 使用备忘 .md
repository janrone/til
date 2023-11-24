
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
