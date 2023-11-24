
### RecyclerView

GridLayoutManager item 居中：   
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
