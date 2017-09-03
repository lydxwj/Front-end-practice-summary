

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
  ​

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