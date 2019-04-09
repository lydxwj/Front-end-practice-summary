

# JavaScript问题

## 1. `void`用法

```javascript
<script>  
	void fun();  
    javascript:void fun();  
//或者是    
	void (fun());  
 	javascript: void(fun());  
</script> 
```

`void` 运算符对任何值返回 `undefined`。该运算符通常用于避免输出不应该输出的值，例如，从 `HTML` 的 `<a>` 元素调用 JavaScript 函数时。要正确做到这一点，函数不能返回有效值，否则浏览器将清空页面，只显示函数的结果。例如：

```html
<a href="javascript:window.open('about:blank')">Click me</a>
```

如果把这行代码放入 `HTML` 页面，点击其中的链接，即可看到屏幕上显示 "[object]"(ie浏览器)。[TIY](http://www.w3school.com.cn/tiy/t.asp?f=jseg_operators_unary_void)

这是因为 `window.open()` 方法返回了新打开的窗口的引用。然后该对象将被转换成要显示的字符串。

要避免这种效果，可以用 `void` 运算符调用 `window.open()` 函数：

```html
<a href="javascript:void(window.open('about:blank'))">Click me</a>
```

这使 window.open() 调用返回 undefined，它不是有效值，不会显示在浏览器窗口中。

**扩展：`href="#" 0` 和 `href="javacript:void(0)`的区别？**

1. 我们在写代码的时候，一个空的链接，我们可能会这样写:`href="#"`。这里的#，它包含了一个位置信息，它默认的锚是`#top（即网页的顶部）`。
2. `javascript:void(0)`仅仅是一个死链接，点击不会有任何效果。通常可以用来取消掉：点击空的`a`链接刷新页面 和 `href="#"`跳到顶部的效果。

# 2. **`&&` 与 `||`易错** 

```javascript
console.log((1>3)&&"abc");                 //  false  因为(1>3)时判断，布尔值
console.log((1<3)&&"abc");                 //  abc
console.log(null&&"abc");                  //  null
console.log(''&&"abc");                    //  ''   空字符串，不是布尔值
console.log((1<3)||"abc");                 //  true
console.log(null||"abc")；                 //  false
console.log(0&&"abc");                     //  0   数字不是布尔值
```

# 3.存在iframe时候事件绑定JQ

- **在iframe子页面获取父页面元素**

      $('#startcp', window.parent.document).click(function (){
      	$(".option.active").removeClass("active");
      });

- **获取iframe中元素**

```javascript
1：document.getElementById("ii").contentWindow 得到iframe对象后，就可以通过contentWindow得到iframe包含页面的window对象，然后就可以正常访问页面元素了；

2：$("#ii")[0].contentWindow  如果用jquery选择器获得iframe，需要加一个【0】；

3：$("#ii")[0].contentWindow.$("#dd").val() 可以在得到iframe的window对象后接着使用jquery选择器进行页面操作;

4：$("#ii")[0].contentWindow.hellobaby="adfsadfsdafsadfdsaffdsaaaaaaaaaaaaa"; 可以通过这种方式向iframe页面传递参数，在iframe页面window.hellobaby就可以获取到值，hellobaby是自定义的变量；

5：在iframe页面通过parent可以获得主页面的window，接着就可以正常访问父亲页面的元素了；

6：parent.$("#ii")[0].contentWindow.ff; 同级iframe页面之间调用，需要先得到父亲的window，然后调用同级的iframe得到window进行操作；
```

## 4.手机端 调用输入法 上的搜索键 进行搜索的使用方法

> **如果基于原生的js或者jq的写法可以如此：**

<form action="javascript:search();">
​         <input type="search" placeholder="请输入搜索内容">
</form>
如果基于angular的写法可以如此：
<form ng-submit="search()">
​         <input type="search" placeholder="请输入搜索内容">
</form>
<script>
​    //跳转的 代码
​    function search(){
​      /*任意发挥*/
​    }
</script>
<style>
​    //隐藏  type=search   自带的 X 按钮
​    ::-webkit-search-cancel-button { display: none; }
</style>

## 5.touch事件冲突

**问题：**

移动端有很多手势事件，移动端浏览器也会有，比如微信中在最顶部下拉会有一个缓冲，uc浏览器，iPhone等，当你的网页中注册了touchmove事件，会造成触发自有的touchmove事件。

**解决：**

在你的网页中的touchmove事件中进行阻止冒泡行为e.stopPropagation()，然而并没有什么用处，即使你把touchstar和touchend都用e.stopPropagation()阻止了默认行为。

这时你应该想到了要阻止默认行为，e.preventDefault()，此时确实可以解决问题，但是处理不好会产生新的问题：点击事件失效，原因是touchstar或者touchend也阻止了默认行为，所以解决只能在touchmove事件阻止默认行为e.preventDefault()。

## 6.Date对象

- **构造函数**

  - `new Date() `返回当前的本地日期和时间
    参数：无

  - `new Date(milliseconds)` ：把毫秒数转换为`Date`对象

    参数：`milliseconds {int}` ：毫秒数；表示从`1970/01/01 00:00:00`为起点，开始叠加的毫秒数。

    注意：起点的时分秒还要加上当前所在的时区，北京时间的时区为东8区，起点时间实际为：'1970/01/01 08:00:00'

  - `new Date(dateStr)`：把字符串转换为`Date`对象

    参数：dateStr {string} ：可转换为Date对象的字符串(可省略时间)；字符串的格式主要有两种：

    1. `yyyy/MM/dd HH:mm:ss` （推荐）：若省略时间，返回的`Date`对象的时间为 00:00:00。
    2. `yyyy-MM-dd HH:mm:ss` ：若省略时间，返回的`Date`对象的时间为 08:00:00(加上本地时区)。若不省略时间，此字符串在IE中会转换失败!

  - `new Date(year, month, opt_day, opt_hours, opt_minutes, opt_seconds, opt_milliseconds)`：把年月日、时分秒转换为Date对象

    参数：

    - `year {int}` ：年份；4位数字。如：1999、2014
    - `month {int}` ：月份；2位数字。从0开始计算，0表示1月份、11表示12月份。
    - `opt_day {int}` 可选：号； 2位数字；从1开始计算，1表示1号。
    - `opt_hours {int}` 可选：时；2位数字；取值0~23。
    - `opt_minutes {int}` 可选：分；2位数字；取值0~59。
    - `opt_seconds {int}` 可选：秒；2未数字；取值0~59。
    - `opt_milliseconds {int}` 可选：毫秒；取值0~999。

> 返回值：

- **get方法**
  - `getFullYear()` ：返回`Date`对象的年份值；4位年份
  - `getMonth()` ：返回`Date`对象的月份值。从0开始，所以真实月份=返回值+1
  - `getDate()` ：返回`Date`对象的月份中的日期值；值的范围1~31
  - `getHours()` ：返回`Date`对象的小时值
  - `getMinutes()` ：返回`Date`对象的分钟值。
  - `getSeconds()` ：返回`Date`对象的秒数值。
  - `getMilliseconds()` ：返回`Date`对象的毫秒值
  - `getDay()` ：返回`Date`对象的一周中的星期值；0为星期天，1为星期一、2为星期二，依此类推
  - `getTime()` ：返回`Date`对象与'1970/01/01 00:00:00'之间的毫秒值(北京时间的时区为东8区，起点时间实际为：'1970/01/01 08:00:00') 。 

- **set方法**
  - `setFullYear(year, opt_month, opt_date)` ：设置`Date`对象的年份值；4位年份
  - `setMonth(month, opt_date)` ：设置`Date`对象的月份值。0表示1月，11表示12月
  - `setDate(date)` ：设置`Date`对象的月份中的日期值；值的范围1~31
  - `setHours(hour, opt_min, opt_sec, opt_msec)` ：设置`Date`对象的小时值
  - `setMinutes(min, opt_sec, opt_msec)` ：设置`Date`对象的分钟值
  - `setSeconds(sec, opt_msec)` ：设置`Date`对象的秒数值
  - `setMilliseconds(msec)` ：设置`Date`对象的毫秒值。

- **其他方法**
  - `toString()` ：将`Date`转换为一个'年月日 时分秒'字符串
  - `toLocaleString()` ：将`Date`转换为一个'年月日 时分秒'的本地格式字符串
  - `toDateString()` ：将`Date`转换为一个'年月日'字符串
  - `toLocaleDateString()` ：将`Date`转换为一个'年月日'的本地格式字符串
  - `toTimeString()` ：将`Date`转换为一个'时分秒'字符串
  - `toLocaleTimeString()` ：将`Date`转换为一个'时分秒'的本地格式字符串
  - `valueOf()` ：与`getTime()`一样， 返回`Date`对象与'1970/01/01 00:00:00'之间的毫秒值(北京时间的时区为东8区，起点时间实际为：'1970/01/01 08:00:00')

- **静态方法**

  -  `Date.now()`

    *说明*：返回当前日期和时间的Date对象与'1970/01/01 00:00:00'之间的毫秒值(北京时间的时区为东8区，起点时间实际为：'1970/01/01 08:00:00') 

    返回值：当前时间与起始时间之间的毫秒数。

  - `Date.parse(dateStr)`

    *说明*：把字符串转换为Date对象 ，然后返回此Date对象与'1970/01/01 00:00:00'之间的毫秒值(北京时间的时区为东8区，起点时间实际为：'1970/01/01 08:00:00')

    参数：

    - `dateStr {string}` ：可转换为Date对象的字符串(可省略时间)；字符串的格式主要有两种：

    1. `yyyy/MM/dd HH:mm:ss` （推荐）：若省略时间，返回的Date对象的时间为 00:00:00。
    2. `yyyy-MM-dd HH:mm:ss` ：若省略时间，返回的Date对象的时间为 08:00:00(加上本地时区)。若不省略时间，此字符串在IE中返回NaN(非数字)!

    返回转换后的Date对象与起始时间之间的毫秒数。

