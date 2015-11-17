# d3.mouse()用法 #
`d3`

d3官网上对该方法介绍：
>##### d3.mouse(container)
Returns the x and y coordinates of the current d3.event, relative to the specified container. The container may be an HTML or SVG container element, such as an svg:g or svg:svg. The coordinates are returned as a two-element array [x, y].

由此可知：

* 该方法的作用是获取当前鼠标相对于某个指定元素的位置信息
* 传入的元素参数是一个HTML元素或者是SVG元素
* 返回值是一个数组元素[x, y],包含鼠标的位置信息

#####方法使用注意：
* 接收的参数container的值是一个HTML元素或者是SVG元素,否则会报错。
参数值结构如下：

	`<g transform="translate(32.5,30)"></g>`

#####例子：
1. 直接传入当前事件元素
	`d3.select('circle').on('click', function() {
		console.log(d3.mouse(this));
	});`
2. 取特定元素

* jQuery:
	`d3.mouse($('circle')[0]);`

* d3:
	`d3.mouse(d3.select('circle')[0][0]);`