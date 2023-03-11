
**Unix 时间戳是从1970年1月1日(UTC/GMT的午夜)开始所经过的秒数,不考虑闰秒。**


iPhone 和 Android 在日期格式方面有所不同。其中，iPhone（iOS）使用的默认日期格式是ISO8601，即“yyyy-MM-dd'T'HH:mm:ss.SSSZ”；而 Android 使用的默认日期格式是“EEE MMM dd HH:mm:ss zzz yyyy”。

要在两个平台之间进行日期格式的统一，可以使用 JavaScript 中的Date对象。 先将日期字符串转为Date对象，然后使用toTimeString()和toDateString()方法将其转换为所需格式。

以下是一个样例代码：

```
let dateString = "2022-03-15T09:30:00.000Z";

let date = new Date(dateString);

// 转化为iPhone格式
let iPhoneDate = date.toISOString();
console.log(iPhoneDate);

// 转化为Android格式
let options = {year: 'numeric', month: 'short', day: 'numeric', hour: 'numeric', minute: 'numeric', second: 'numeric', timeZoneName: 'short'};
let AndroidDate = date.toLocaleDateString("en-US", options);
console.log(AndroidDate);
```

输出结果：
```
iPhone格式： "2022-03-15T09:30:00.000Z"
Android格式： "Mar 15, 2022, 5:30:00 PM PDT"
```
通过这种方法，可以将日期转换为在两个平台上都可用的格式。

---
### 如何创建一个标准的时间

在 JavaScript 中，Date 对象可以通过不同的方法来创建，其中一种方法是传递时间戳值（即 UTC 时间距离 Unix 时间戳的毫秒数）。

因此，我们可以在代码中使用 Date.now() 方法来获取当前时间的时间戳，并将其传递给Date()构造函数，从而创建一个与当前时间对应的 Date 对象。这种方法可以在 iOS 和 Android 设备上都获得相同的结果。

以下是一个示例代码：

```
// 获取当前时间的时间戳
const timestamp = Date.now();

// 使用时间戳创建一个Date对象
const date = new Date(timestamp);

// 输出日期对象的字符串形式
console.log(date.toISOString());
```

输出结果：

```
2022-03-21T02:59:12.842Z
```
还有其他一些方法可以创建 Date 对象，如传递日期字符串或日期的年、月、日等值。但是，由于不同操作系统或浏览器可能会将日期字符串解析为不同的格式，
因此在进行跨平台开发时，建议使用上述方法，即传递时间戳值来创建 Date 对象。

---
### 时间戳转标准时间

在 JavaScript 中，可以使用 Date 对象将时间戳转换为标准的时间格式。使用 Date() 构造函数创建一个 Date 对象，将时间戳作为参数传递给构造函数即可。

以下是一个示例代码，演示了如何将时间戳转换为标准的时间格式：

```
// 定义一个时间戳
const timestamp = 1647925828000; // 这个时间戳代表 2022-03-21T02:03:48.000Z

// 创建 Date 对象
const date = new Date(timestamp);

// 输出格式化之后的时间
console.log(date.toLocaleString()); // 默认输出本地时间格式
console.log(date.toISOString()); // 输出标准的 ISO 8601 时间格式
console.log(date.toUTCString()); // 输出 UTC 时间格式
```
输出结果：

```
2022/3/21 下午10:03:48 (本地时区格式)
2022-03-21T02:03:48.000Z (标准的 ISO 8601 时间格式)
Mon, 21 Mar 2022 02:03:48 GMT (UTC 时间格式)
```
在这个示例中，我们首先定义了一个时间戳（即UTC时间距Unix时间戳的毫秒数），然后使用 new Date(timestamp) 创建了一个 Date 对象。

接着，我们使用 toLocaleString() 方法将日期对象转化为本地时间格式的字符串，使用 toISOString() 方法将其转化为标准的 ISO 8601 时间格式，使用 toUTCString() 方法将其转化为 UTC 时间格式。这三种方法会返回不同的时间格式的字符串。

这种方法适用于将时间戳转换为标准的时间格式，使其更易于阅读和理解的情况。

### 总结
 - 我们传递和储存时间一律使用时间戳。
 - 在 JS 中可以使用 date.toISOString(); // 输出标准的 ISO 8601 时间格式

