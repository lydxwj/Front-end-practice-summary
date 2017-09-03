# 与数组相关

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
# 与字符串相关

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

# 易混淆宽高

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

# 文件读取

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

# 文件拖拽

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

# 文件拖拽读取

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
# 浏览器存储

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

# 定位

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
# 视频播放

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
