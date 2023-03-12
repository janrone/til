**我写小程序的时候突然需要根据不同的值给 json 设置不同的 key ，值的设置是我知道，但 key 之前没设置过，试用了下 value 设置的方式是不可以的，
后查询之后发现需要加 [] 方括号。 之后就有了这篇文章 。**

```
  type: data.url ? 'qrcode' : 'image',
  [data.url ? 'content' :  'url'] : data.url ? data.url : '/palette/mini_ihools_code_n.jpg'
```

---


在 JavaScript 中，我们可以使用 JSON 对象来存储和操作数据，JSON 对象是一种轻量级的数据格式，常用于前后端数据交互。

在使用 JSON 对象时，我们通常会在定义 JSON 对象时就确定好其 Key 值，例如：

```
const person = {
  name: '张三',
  age: 18,
  gender: 'male'
}
```
但是，在某些情况下，我们需要动态地给 JSON 对象的 Key 赋值，例如，我们需要根据用户输入的数据来动态创建 JSON 对象的 Key，这时我们可以使用方括号语法来动态赋值。

```
const key = 'name';
const person = {};
person[key] = '张三';
console.log(person); // {name: "张三"}
```
在上面的代码中，我们定义了一个变量 key，并将其赋值为字符串 'name'，然后通过方括号语法将 key 作为 JSON 对象的 Key，最终得到了一个包含了动态 Key 的 JSON 对象。

除了使用方括号语法外，我们还可以使用 ES6 中的计算属性名语法来动态赋值，例如：

```
const key = 'name';
const person = {
  [key]: '张三'
};
console.log(person); // {name: "张三"}
```
在上面的代码中，我们使用了计算属性名语法，将变量 key 作为 JSON 对象的 Key，最终得到了一个与上面例子相同的 JSON 对象。

总的来说，使用方括号语法和计算属性名语法都可以在 JavaScript 中实现 JSON Key 的动态赋值，具体使用哪种方式，可以根据具体的需求和场景来选择。
