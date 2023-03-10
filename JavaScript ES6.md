const { pathname, search } = url
这行代码使用了解构赋值语法，将url对象的pathname和search属性分别赋值给了变量pathname和search。

这相当于按以下方式提取对象属性并将它们存储在变量中：

```
const pathname = url.pathname;
const search = url.search;
```


通过使用解构赋值，可以简化这个过程，这也是 JavaScript ES6 中的一种语法糖。
