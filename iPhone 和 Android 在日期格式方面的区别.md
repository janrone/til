
**整篇文章由iPhone 和 Android 在日期格式方面有所不同引起，大致介绍了，两种时间标准，以及在 JavaScript 下的格式转换方法。**

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

### 不同时区转换

在JavaScript中，可以使用Date对象将CST时间和UTC时间之间进行相互转换。以下是一个将CST时间转换为UTC时间的示例代码：

```
// 指定CST时间字符串（例如2021-08-10 12:30:15）
let cst_time_str = '2021-08-10 12:30:15';

// 将CST时间字符串转换为Date对象，并指定时区为CST (-6:00)
let cst_time = new Date(cst_time_str + ' GMT-0600');

// 将CST时间转换为UTC时间，并格式化为UTC时间字符串
let utc_time_str = cst_time.toISOString();
console.log("转换后的UTC时间：", utc_time_str);
```

输出结果：

```
转换后的UTC时间： 2021-08-10T18:30:15.000Z
```

这里先将CST时间字符串转换为Date对象，并通过指定时区为CST（GMT-0600）来确保正确解析时间。然后，将CST时间转换为UTC时间，并使用toISOString()方法将其格式化为UTC时间字符串。

以下是一个将UTC时间转换为CST时间的示例代码：

```
// 指定UTC时间字符串（例如2021-08-10T04:30:15.000Z）
let utc_time_str = '2021-08-10T04:30:15.000Z';

// 将UTC时间字符串转换为Date对象
let utc_time = new Date(utc_time_str);

// 将UTC时间转换为CST时间，并格式化为CST时间字符串
let cst_time_str = utc_time.toLocaleString('en-US', {timeZone: 'America/Chicago'});
console.log("转换后的CST时间：", cst_time_str);

// 'zh-cn' //zh-hans
//TIME_ZONE = 'Asia/Shanghai'
cst_time_str = utc_time.toLocaleString('zh-cn', {timeZone: 'Asia/Shanghai'});
console.log("转换后的CST时间：", cst_time_str);

```

输出结果：

```
转换后的CST时间： 8/9/2021, 11:30:15 PM

转换后的CST时间： 2021/8/10 12:30:15
```

这里先将UTC时间字符串转换为Date对象。然后，利用toLocaleString()方法，将UTC时间转换为美国中部时区（'America/Chicago'）的本地时间，并进行格式化为CST时间字符串。

CST可视为美国、澳大利亚、古巴或中国的标准时间。CST可以为如下4个不同的时区的缩写：  

1、美国中部时间：CentralStandardTime（USA）UT-6:00；  
2、澳大利亚中部时间：CentralStandardTime（Australia）UT+9:30；  
3、中国标准时间：ChinaStandardTimeUT+8:00；  
4、古巴标准时间：CubaStandardTimeUT-4:00。  

### 总结
 - 我们传递和储存时间一律使用时间戳。
 - 在 JS 中可以使用 date.toISOString(); // 输出标准的 ISO 8601 时间格式
 - 不同时区转换可以通过设置timeZone来实现
 
---

### 时间标准

- 世界标准时间（UTC）协调世界时（英：Coordinated Universal Time ，法：Temps Universel Coordonné），又称世界统一时间，世界标准时间，国际协调时间。英文（CUT）和法文（TUC）的缩写不同，作为妥协，简称 UTC。它是目前国际上广泛采用的精确时间标准。UTC 是建立在原子钟技术基础之上的，以国际原子时为基础，每秒恒等于9,192,631,770个原子振动周期的时间单位。

 
  世界标准时间UTC：GMT+0

- 格林威治时间（GMT）是指在英国伦敦的本初子午线上，以24小时制度所示的时间。过去，GMT 曾是国际上通用的时间标准，但随着科技进步和航空旅行的需求，逐渐改为更为精确的时间标准。
世界时UT 即格林尼治时间，格林尼治所在地的标准时间。

  以地球自转为基础的时间计量系统。地球自转的角度可用地方子午线相对于地球上的基本参考点的运动来度量。为了测量地球自转，人们在地球上选取了两个基本参考点：春分点（见分至点）和平太阳，由此确定的时间分别称为恒星时和平太阳时。

  但是格林尼治本地的时间比格林尼治平时，大一小时，也就是格林尼治本地的时间：GMT+1

两者的区别在于，GMT 是按太阳高度的变化来计算时间的，而 UTC 是一种原子钟制时间标准，更为精确和准确。此外，UTC 使用了闰秒的方法来保持与地球自转周期的匹配，而 GMT 则不考虑地球自转周期和夏令时等因素的变化，因此 UTC 更为准确和实用。



