# learning bootstrap popover #

#### HTML属性配置

* data-toggle: 标识弹出框元素
* title: 弹出框标题
* data-content: 弹出框内容
* data-placement: 弹出框位置【left/top/bottom/right/auto】
* data-container: 弹出框所在位置
* data-trigger: 添加该属性使点击弹出框会让弹出框消失
* ...

#### 例子
eg: 简单的弹出框

```
<button type="button" class="btn btn-lg btn-danger" data-trigger="focus" data-placement='bottom' data-toggle="popover" title="Popover title" data-content="And here's some amazing content. It's very engaging. Right?">点我弹出/隐藏弹出框</button>
<script type="text/javascript">
	$('button').popover();
</script>
```

#### 使用js进行配置
初始化参数：

* animation(同data-animation): [boolean] 是否为弹出框赋予CSS效果（默认为true）
* container(同data-container): [string/false] 添加弹出框的位置（常用`container`）
* content(同data-content): [string/function] 弹出框内容
* delay(同data-delay): [number/object] 显示/隐藏延迟时间(eg: {show: 500, hide: 100} HTML标签数字没问题，对象未起作用)
* html(同data-html): [boolean] 是否可以在弹出框中添加HTML元素，默认false时仅当普通文本
* placement(同data-placement): [string/function] 弹出框位置【left/top/bottom/right/auto】
* title: [string/function] 弹出框的标题
* trigger: [string] 弹出框的触发方式【click/hover/focus/manual】除`manual`外可以多个进行组合(以空格隔开)

//not very clear now
* selector: [string]
* template: [string] 创建弹出框的模板
* viewport：[string/object/function] 

常用方法：

1. $().popover(options) 初始化弹出框
2. $().popover('show') 显示弹出框
3. $().popover('hide') 隐藏弹出框
4. $().popover('toggle') 切换显示、隐藏
5. $().popover('destroy') 销毁弹出框

eg: 使用js创建简易弹出框
```
<button type="button" class="btn btn-lg btn-danger" data-trigger="hover" >弹出/隐藏弹出框</button>
<script type="text/javascript">
	$('button').popover({
		content: 'here is the content'
	});
</script>
```