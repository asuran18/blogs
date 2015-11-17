# d3.transform()用法 #
`d3` `2D Transforms`

使用过D3的都知道，SVG元素存在一个属性`transform`,它的值代表该SVG元素的位置偏移、旋转、缩放及倾斜度。有时我们需要该属性值中的部分信息，可能是偏移、也可能是旋转的值。因此D3中也提供了这样一个方法`d3.transform`。

>d3.transform(string)

这是在d3的API中对该方法的定义，接收一个字符串类型的参数，该参数为SVG元素的`transform`属性的值。该方法的返回值为一个对象，该对象包含了偏移、旋转等所有信息。

#####方法返回值的结构如下：

	{
		'rotate': [Number],
		'scale': [Array],
		'skew': [Number],
		'translate': [Array]
	}

基于该方法的返回值，API中定义了以下方法用来取对应的值（实际上就是直接获取对象的值）

1. transform.rotate -- 获取旋转的角度
2. transform.translate -- 获取偏移值
3. transform.skew -- 获取倾斜度
4. transform.scale -- 获取缩放比例
5. transform.toString() -- 对该变换值的展示

####直接读取SVG元素`attr('transform')`的值和使用`transform.toString()`获取的值的不同

* 直接读取SVG元素`attr('transform')`的值为`translate(50,50)`

* 使用`transform.toString()`获取的值为`translate(50,50)rotate(0)skewX(0)scale(1,1)`

由此可知，通过`transform.toString()`获取的值较为全面，显示当前元素的所有属性，而直接读取属性值获得的是当前元素被改变的属性。在平时使用中，直接使用`attr('transform')`属性获取的值就足够了。