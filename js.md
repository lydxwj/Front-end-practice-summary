

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

## 7.与数组相关

```jsx
var	arr1=[4,5,2,6,3];
var	arr2=[9,7,0,9];
arr1.concat(arr2);					//两个数组组合拼接
var str=arr1.join("-");			//用符号-连接数组每一项，得到字符串
str.split("-");					//把字符串中-每一段，分为数组每一项
arr1.reverse();					//倒序排列数组
function reFn(a,b){
  return (a-b);
}
arr1.sort(reFn);				//从小到大排序
arr1.splice(0,2,3,4);			//从索引0开始删除2个，再在删除的地方插入3,4，此方法会修改原数组
arr1.slice(0,2);				//从索引0开始，截取到索引2，[0,2)能取到0，取不到2
arr1.push(1);					//从数组arr1后面添加一项
arr1.pop();						//从数组arr1后面删除一项
arr1.unshift(1);				//从数组arr1前面添加一项
arr1.shift();					//从数组arr1前面删除一项
arr1.indexOf(2);				//从数组arr1中查找2，返回第一个2的索引，没有则返回-1
arr1.indexOf(2,1);				//从数组arr1中索引1开始查找2，返回第一个2的索引，没有则返回-1
arr1.lastIndexOf(2);			//从数组arr1中最后面开始查找2，返回第一个2的索引，没有则返回-1
arr1.findIndex(function(x) {
  return (x == 2);
});							//2	返回第一个符合条件的数组成员的位置
arr1.findIndex(function(value, index, arr) {  
	return value > 5;  
})							 // 3  返回第一个符合条件的数组成员的位置
var arrNew=arr1.filter(function(el,index,arr){
  	if(el>4){
      return false;
  	}
  	return true;
});								//数组筛选，返回true的保留
arr1.forEach(function(el,index,arr){
  	console.log(el);
});								//数组遍历
var arrNew = arr1.map((currentValue, index, array) => {
    console.log(`currentValue = `, currentValue);
    console.log(`index = `, index);
    console.log(`array= `, array);
    return currentValue * 2;
}, arr1);	//对数组每一项进行遍历操作，最后一个参数arr1（可选），表示回调函数中this指向
arr1.find((n) => n < 4);		//2	 找出第一个符合条件的数组成员
arr1.find(function(value, index, arr) {  
	return value >4;  
}) // 5   找出第一个符合条件的数组成员
arr1.every(function(e){
  return (e>5);
});		//false  检测数组所有元素是否都符合指定条件
arr1.every(function(e){
  return (e>5);
});		//true  用于检测数组中的元素是否满足指定条件,有一个就可以
```

## 8.与字符串相关

```jsx
var str="hello world";
str.slice(4,7);             //o w  起始位置和结束位置(不包括结束位置)
str.substring(4,7);         //o w	起始位置和结束位置(不包括结束位置)
str.substring(7,4);         //o w	较小的为起始位置，较大的为结束位置
str.substr(4,7);            //o world  起始位置和所要返回的字符串长度
str.search('ll');			//2	检索字符串中指定的子字符串，或检索与正则表达式相匹配的子字符串
//--------------------------------------------
str.slice(-3);              //rld	将它字符串的长度与对应的负数相加，结果作为参数
str.slice(3,-4);       		//lo w 将它字符串的长度与对应的负数相加，结果作为参数

str.substring(-3);     		//hello world	将负参数都直接转换为0
str.substring(3,-4);   		//hel	将负参数都直接转换为0

str.substr(-3);        		//rld	将第一个参数与字符串长度相加后的结果作为第一个参数
str.substr(3,-4);      		//空字符串	将第一个参数与字符串长度相加后的结果作为第一个参数
//-----------------------------------------------------------------
str.indexOf("e");			//1 第一个匹配的字符串索引位置
str.replace("o","!");		//只会替换第一个匹配的o字符串替换为！
str.replace(/o/g,"!");		//替换所有匹配的o字符串替换为！
str.charAt(2);				//l 指定索引位置2处的字符
var str2=str.toUpperCase();	//HELL0 WORLD 变成大写字符串
str2.toLowerCase();			//hello world 变成小写字符串
```

## 9.易混淆宽高

```jsx
screen.width			//屏幕显示器的宽度(分辨率值) 
screen.height			//屏幕显示器的高度(分辨率值) 内容可视区域的高度
el.offsetWith			//获取自身宽   border+padding+width 不带单位，只能获取
//-------------------------------------------------------
el.offsetHeight			//获取自身高   
el.offsetParent			//获取自身最近的带有定位的父级元素对象
el.offsetLeft			//获取自身左边距离最近的带有定位的父级的距离  父padding+自margin 以border左上角为基准
//-------------------------------------------------------
el.scrollHeight			//对象内部实际内容的高度，会超过盒子
el.scrollWidth			//对象内部实际内容的宽度
el.scrollTop			//对象滚动轴滚动顶部距离
el.scrollLeft			//对象滚动轴滚动左侧距离
//-------------------------------------------------------
el.clientHeight			//内容可视区域的高度，不包含border
el.clientWidth			//内容可视区域的宽度
el.clientTop			//顶部border宽度
el.clientLeft			//左侧border宽度	
```

## 10.文件读取

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title></title>
		<style>
			.iconBox{
				width: 200px;
				height: 200px;
				border:5px dashed red;
			}
			.container{
				display: flex;
			}
		</style>
	</head>
	<body>
		<h1>请选择您的头像</h1>
		<div class='container'>
			<input type="file"  id="selectFile" />
			<div class='iconBox'></div>
		</div>
	</body>
</html>
<script type="text/javascript">
	document.querySelector('input[type=file]').onchange = function (){
//		console.log('123')		
		// 创建文件读取对象
		var reader = new FileReader();	
		// 通过当前的file标签 获取选择的文件
		console.log(this.files);	
		// 调用该对象的方法读取文件 文件
		// 读取文件是一个耗时操作 不一定什么时候读取完毕
		reader.readAsDataURL(this.files[0]);		
		// 添加事件
		// 耗时操作 通过事件的方式进行注册 并且回调
		reader.onload = function (){
			// 使用读取完毕的文件
			console.log(reader.result);
			//使用返回的结果 即可
			document.querySelector('.iconBox').style.background = 'url('+ reader.result+') no-repeat center/cover';
		}	
	}
</script>
```

## 11.文件拖拽

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title></title>
		<style>
			body{
				text-align: center;
			}
			img{
				margin: 0 10px;
				border:1px solid gray;
			}
			.colorBlock{
				display: flex;
				justify-content: center;
			}
			.colorBlock>div{
				width: 100px;
				height: 100px;
				border:1px solid gray;
				margin:0 10px;
			}
			.colorBlock>div:nth-child(1){
				background-color: red;
			}
			.colorBlock>div:nth-child(2){
				background-color: skyblue;
			}
			.colorBlock>div:nth-child(3){
				background-color: yellowgreen;
			}
			.showBox{
				margin: 10px auto;
				width: 100px;
				height: 100px;
				border:5px dashed black;
			}
		</style>
	</head>
	<body>
		<h1>默认支持拖拽的元素</h1>
			<img src="images/lf.jpg" alt="" />
			<img src="images/sl.jpg" alt="" />
			<img src="images/nm.jpg" alt="" />
		<h1>开启拖拽</h1>
		<div class="colorBlock">
			<div draggable="true"></div>
			<div draggable="true"></div>
			<div draggable="true"></div>
		</div>
		<h1>展示区域</h1>
		<div class='showBox'></div>
	</body>
</html>
<script type="text/javascript">
	var moveDom;
	// 为所有的img 绑定点击事件
	var imgs = document.querySelectorAll('img');	
	// 循环绑定点击事件
	for (var i = 0 ; i < imgs.length ; i++) {		
		imgs[i].ondragstart = function () {
			moveDom = this;
		}
	}	
	// 为所有的颜色div绑定拖拽事件
	var colorDivs = document.querySelectorAll('.colorBlock>div');	
	// 循环绑定拖拽事件
	for (var i = 0 ; i <colorDivs.length;i++) {
		colorDivs[i].ondragstart = function () {
			moveDom = this;
		}
	}
	// 允许拖入
	document.querySelector('.showBox').ondragover = function (e) {
		e.preventDefault();
	}
	// 拖入的元素松手时调用
	document.querySelector('.showBox').ondrop = function (e) {
		// 判断是否有src属性
		if (moveDom.src) {
			this.style.background = 'url('+ moveDom.src +')';
		}else{
			console.log(getComputedStyle(moveDom).backgroundColor);
			this.style.background = getComputedStyle(moveDom).backgroundColor;
		}
	}
</script>
```

## 12.文件拖拽读取

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title></title>
		<style type="text/css">
			html,body{
				height: 100%;
			}
			body{
				/*body元素 默认就是一个盒子 是没有高度的*/
				border:10px dashed gray;
				margin: 0;
			}
		</style>
	</head>
	<body>
	</body>
</html>
<script type="text/javascript">
	//  ondragover 目的是为了让 元素的 ondrop事件能够被触发
	document.body.ondragover = function(e){
		e.preventDefault();
	}
	// ondrop 想要被触发 必须 在ondragover事件中 组织默认行为
	document.body.ondrop = function (e){
//		console.log('123');
		e.preventDefault();
		console.log(e.dataTransfer.files[0]);		
		// 创建文件读取对象
		var reader = new FileReader();	
		// 调用文件读取方法
		reader.readAsDataURL(e.dataTransfer.files[0]);	
		// 在文件读取完毕事件中 获取结果
		reader.onload = function (){
			document.body.style.background = 'url('+reader.result+')no-repeat center/cover';
		}		
	}
</script>
```

## 13.浏览器存储

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title></title>
		<style>
			.container{
				display: flex;
				justify-content: center;
			}
			.container>div{
				height: 100px;
				width: 100px;
				margin:0 10px;
				border:1px solid gray;
			}
			.red{
				background-color: red;
			}
			.orange{
				background-color: orange;
			}
			.yellowgreen{
				background-color: yellowgreen;
			}
			body{
				text-align: center;
			}
			input{
				margin:0 5px;
			}
		</style>
	</head>
	<body>
		<div class='container'>
			<div class='red'></div>
			<div class='orange'></div>
			<div class='yellowgreen'></div>
		</div>
		<input type="button" value='保存'/>
		<input type="button" value='读取'/>
		<input type="button" value='清除'/>
	</body>
</html>
<script type="text/javascript">
	// 获取三个div
	var colorDivs = document.querySelectorAll('.container>div');
	for (var i= 0;i<colorDivs.length ;i++) {
		colorDivs[i].onclick = function (){
			// 获取自己 在style标签中的颜色 设置给 body
			document.body.style.backgroundColor = getComputedStyle(this).backgroundColor;
		}
	}	
	/*localStorage 保存的值 关闭浏览器之后 还是存在的
	 	sessionStorage 保存的值 关闭浏览器之后 就没有了*/	
	// 保存数据
	document.querySelector('input[value=保存]').onclick = function(){
		// 只能保存字符串 这里保存的是 body的 背景颜色
		window.localStorage.setItem('myColor',getComputedStyle(document.body).backgroundColor);
		// 演示另外一种保存的方法											window.sessionStorage.setItem('myColor',getComputedStyle(document.body).backgroundColor);
		alert('保存成功');
	}
	// 读取数据
	document.querySelector('input[value=读取]').onclick = function(){
		// 传入key 即可获取保存的内容
		var result = window.localStorage.getItem('myColor');
		document.body.style.backgroundColor = result;
		alert('读取成功');
	}	
	// 删除数据
	document.querySelector('input[value=清除]').onclick = function(){
		// 清除数据 指定删除某一个键对应的值
//		window.localStorage.removeItem('myColor');
		// 如果我们只想 删除某一个的话 使用removeItem的方法即可
		window.localStorage.clear();
		alert('清除成功');
	}	
	// 打开浏览器 如果保存了颜色 那么直接加载改颜色
	window.onload = function (){
		var color =window.localStorage.getItem('myColor');
		if(color!=null){
			document.body.style.backgroundColor = color;
		}else{
			alert("没有保存颜色哦");
		}
	}
</script>
```

## 14.定位

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title></title>
	</head>
	<body>
		<input type="button"  value='获取位置信息'/>
	</body>
</html>
<script type="text/javascript">
	document.querySelector('input[value=获取位置信息]').onclick = function(){
		// 
		// 参数1:定位成功的回调方法
		// 参数2:定位失败的回调方法
		// 参数3:一些定位的选项
		window.navigator.geolocation.getCurrentPosition(function(position){
//			console.log(position);
			console.log('位置获取成功');
			console.log('经度:'+position.coords.longitude);
			console.log('纬度:'+position.coords.latitude);
		})
	}
</script>
```

## 15.视频播放

```jsx
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title></title>
		<link rel="stylesheet" type="text/css" href="css/font-awesome.min.css"/>
		<style type="text/css">
			.container{
				width: 500px;
				height: 300px;
				background-color: black;
				margin: 100px auto;
			}
			.video{
				width: 100%;
				height: 90%;
			}
			.video video{
				width: 100%;
				height: 100%;
			}
			.controler{
				display: flex;
				align-items: center;
			}
			.controler .progress {
				height: 15px;
				background: white;
				flex:1;
			}
			.controler .progress .step{
				width: 0%;
				height: 100%;
				background: gray;
			}
			.controler a{
				font-size:20px;
				color:whitesmoke;
				margin:0 5px;
			}
		</style>
	</head>
	<body>
		<div class="container">
			<div class="video">
				<video src="movie/bglb.mp4"></video>
			</div>
			<div class="controler">
				<a href="#" class='icon-play-circle' id='play'></a>
				<div class="progress">
					<div class="step"></div>
				</div>
				<a href="#" class='icon-fullscreen' id='fullScreen'></a>
			</div>
		</div>
	</body>
</html>
<script type="text/javascript">
	// 获取video标签
	var videoDom = document.querySelector('video');	
	// 播放暂停
	document.querySelector('#play').onclick = function (){
		//		videoDom.play();
			if(this.classList.contains('icon-pause')){
				// 暂停视频播放
				videoDom.pause();
				// 移除 暂停class即可
				this.classList.remove('icon-pause');
			}else{
					// 播放
				videoDom.play();
				// 添加 暂停图标
				this.classList.add('icon-pause');
			}	
	}
	// 更新进度 测试事件 触发一次
	videoDom.onplay = function (){
		console.log('播放中');
	}
	videoDom.ontimeupdate = function(){
		console.log('播放中1111')
		// 计算进度信息
		console.log(videoDom.currentTime / videoDom.duration);
		// 换算成百分比 设置给 进度条 底部的 进度信息即可
		var percent = videoDom.currentTime / videoDom.duration *100 +'%';
		document.querySelector('.step').style.width =percent;
	}	
	// 进度条 添加点击事件
	document.querySelector('.progress').onclick = function (e){
		console.log(e.offsetX);
		console.log(this.clientWidth);		
		// 修改 进度信息 即可
		// 这个值是字符串
		var percent = e.offsetX / this.clientWidth *100 +"%";
		document.querySelector('.step').style.width =percent;	
		// 修改 视频当前播放的一个 时间
		videoDom.currentTime = videoDom.duration * e.offsetX / this.clientWidth;
	}	
	// 切换全屏
	document.querySelector('#fullScreen').onclick = function (){
		if(videoDom.requestFullscreen){
			videoDom.requestFullscreen();
		}else if(videoDom.webkitRequestFullScreen){
			videoDom.webkitRequestFullScreen()
		}else if(videoDom.msRequestFullscreen){
			videoDom.msRequestFullscreen();
		}else if(this.mozRequestFullScreen){
			videoDom.mozRequestFullScreen();
		}
	}
</script>

```