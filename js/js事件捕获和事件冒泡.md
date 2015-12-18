# js 事件冒泡和事件捕获 #

#### 基础了解

* 事件捕获：由外层向内（到目标元素为止）一层层传递时触发
* 事件冒泡：由目标元素向外一层层传递时触发

添加事件的方法：
>`addEventListener(event, fn, useCapture)`
  - event: 事件类型，如'click'
  - fn: 触发事件时执行的函数
  - useCapture: 是否使用事件捕获（值为true时，事件会在捕获阶段被触发；值为false，事件会在冒泡阶段被触发）

阻止事件冒泡的方法：`event.stopPropagation()`

#### 例子
对以下HTML元素：
```
	<div id="c1">
		<div id="c2">
			<button id="target">test</button>
		</div>
	</div>
```

eg1: 简单事件捕获
js代码：
```
document.getElementById('c1').addEventListener('click', function() {
	console.log('-------- 1 --------');
}, true);
document.getElementById('c2').addEventListener('click', function() {
	console.log('-------- 2 --------');
}, true);
document.getElementById('target').addEventListener('click', function() {
	console.log('-------- target --------');
}, true);
```
结果为：
>-------- 1 --------
 -------- 2 --------
 -------- target --------
 由外层向内一层层触发

 eg2: 简单事件冒泡
js代码：
```
document.getElementById('c1').addEventListener('click', function() {
	console.log('-------- 1 --------');
}, false);
document.getElementById('c2').addEventListener('click', function() {
	console.log('-------- 2 --------');
}, false);
document.getElementById('target').addEventListener('click', function() {
	console.log('-------- target --------');
}, false);
```
结果为：
>-------- target --------
 -------- 2 --------
 -------- 1 --------
 由内层向外一层层触发

eg3: 阻止事件冒泡
js代码：
```
document.getElementById('c1').addEventListener('click', function() {
	console.log('-------- 1 --------');
}, false);
document.getElementById('c2').addEventListener('click', function() {
	console.log('-------- 2 --------');
}, false);
document.getElementById('target').addEventListener('click', function() {
	console.log('-------- target --------');
	event.stopPropagation()
}, false);
```
结果为：
>-------- target --------
 仅触发了目标元素的事件
