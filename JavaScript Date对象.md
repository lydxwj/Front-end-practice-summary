# **JavaScript Date对象**

## **构造函数**

### 1. `new Date()` ：返回当前的本地日期和时间

> *参数：*无
>
> 返回值

- {Date} 返回一个表示本地日期和时间的Date对象。

### 2. **`new Date(milliseconds)` ：把毫秒数转换为`Date`对象**

> 参数：

- `milliseconds {int}` ：毫秒数；表示从`1970/01/01 00:00:00`为起点，开始叠加的毫秒数。

**注意：起点的时分秒还要加上当前所在的时区，北京时间的时区为东8区，起点时间实际为：'1970/01/01 08:00:00'**

> 返回值：

- {Date} 返回一个叠加后的Date对象。

### 3. `new Date(dateStr)` ：把字符串转换为`Date`对象

> 参数：

- dateStr {string} ：可转换为Date对象的字符串(可省略时间)；字符串的格式主要有两种：

1. `yyyy/MM/dd HH:mm:ss` （推荐）：若省略时间，返回的`Date`对象的时间为 00:00:00。
2.  `yyyy-MM-dd HH:mm:ss` ：若省略时间，返回的`Date`对象的时间为 08:00:00(加上本地时区)。若不省略时间，此字符串在IE中会转换失败!

> 返回值：

- {Date} 返回一个转换后的Date对象。

### 4. `new Date(year, month, opt_day, opt_hours, opt_minutes, opt_seconds, opt_milliseconds)` ：把年月日、时分秒转换为`Date`对象

> 参数：

- `year {int}` ：年份；4位数字。如：1999、2014
- `month {int}` ：月份；2位数字。从0开始计算，0表示1月份、11表示12月份。
- `opt_day {int}` 可选：号； 2位数字；从1开始计算，1表示1号。
- `opt_hours {int}` 可选：时；2位数字；取值0~23。
- `opt_minutes {int}` 可选：分；2位数字；取值0~59。
- `opt_seconds {int}` 可选：秒；2未数字；取值0~59。
- `opt_milliseconds {int}` 可选：毫秒；取值0~999。

> 返回值：

- {Date} 返回一个转换后的Date对象。

## **get方法**

1.  `getFullYear()` ：返回`Date`对象的年份值；4位年份。
2.  `getMonth()` ：返回`Date`对象的月份值。从0开始，所以真实月份=返回值+1 。
3.  `getDate()` ：返回`Date`对象的月份中的日期值；值的范围1~31 。
4.  `getHours()` ：返回`Date`对象的小时值。
5.  `getMinutes()` ：返回`Date`对象的分钟值。
6. `getSeconds()` ：返回`Date`对象的秒数值。
7.  `getMilliseconds()` ：返回`Date`对象的毫秒值。
8.  `getDay()` ：返回`Date`对象的一周中的星期值；0为星期天，1为星期一、2为星期二，依此类推
9. `getTime()` ：返回`Date`对象与'1970/01/01 00:00:00'之间的毫秒值(北京时间的时区为东8区，起点时间实际为：'1970/01/01 08:00:00') 。 

## **set方法**

1. `setFullYear(year, opt_month, opt_date)` ：设置`Date`对象的年份值；4位年份。
2. `setMonth(month, opt_date)` ：设置`Date`对象的月份值。0表示1月，11表示12月。
3. `setDate(date)` ：设置`Date`对象的月份中的日期值；值的范围1~31 。
4. `setHours(hour, opt_min, opt_sec, opt_msec)` ：设置`Date`对象的小时值。
5. `setMinutes(min, opt_sec, opt_msec)` ：设置`Date`对象的分钟值。
6. `setSeconds(sec, opt_msec)` ：设置`Date`对象的秒数值。
7. `setMilliseconds(msec)` ：设置`Date`对象的毫秒值。

 

## **其他方法**

1. `toString()` ：将`Date`转换为一个'年月日 时分秒'字符串
2. `toLocaleString()` ：将`Date`转换为一个'年月日 时分秒'的本地格式字符串
3. `toDateString()` ：将`Date`转换为一个'年月日'字符串
4. `toLocaleDateString()` ：将`Date`转换为一个'年月日'的本地格式字符串
5. `toTimeString()` ：将`Date`转换为一个'时分秒'字符串
6. `toLocaleTimeString()` ：将`Date`转换为一个'时分秒'的本地格式字符串
7. `valueOf()` ：与`getTime()`一样， 返回`Date`对象与'1970/01/01 00:00:00'之间的毫秒值(北京时间的时区为东8区，起点时间实际为：'1970/01/01 08:00:00')

## **静态方法**

### 1. `Date.now()`

- *说明*：返回当前日期和时间的Date对象与'1970/01/01 00:00:00'之间的毫秒值(北京时间的时区为东8区，起点时间实际为：'1970/01/01 08:00:00') 

> *参数：*无

> 返回值：

- {int} ：当前时间与起始时间之间的毫秒数。

### 2. `Date.parse(dateStr)`

- *说明*：把字符串转换为Date对象 ，然后返回此Date对象与'1970/01/01 00:00:00'之间的毫秒值(北京时间的时区为东8区，起点时间实际为：'1970/01/01 08:00:00')

> 参数：

- `dateStr {string}` ：可转换为Date对象的字符串(可省略时间)；字符串的格式主要有两种：

1. `yyyy/MM/dd HH:mm:ss` （推荐）：若省略时间，返回的Date对象的时间为 00:00:00。
2. `yyyy-MM-dd HH:mm:ss` ：若省略时间，返回的Date对象的时间为 08:00:00(加上本地时区)。若不省略时间，此字符串在IE中返回NaN(非数字)!

> 返回值：

- {int} 返回转换后的Date对象与起始时间之间的毫秒数。

 