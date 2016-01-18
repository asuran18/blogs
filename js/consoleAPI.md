# js consoleAPI 相关 #

#### 1. 常用
##### 1.1 console.log
>最常用，在控制台打印一些信息(可同时打印多个对象)。
还可以接受变量作为参数传递到字符串中，其具体语法与C语言中的printf语法一致。
%s 表示输出字符串
%d 表示输出数字（也可以用%i）
%f 表示输出浮点数值
%o 表示输出Dom元素
%O 表示输出JavaScript对象
%c 表示对输出的文字应用特殊的样式
```
eg: 
var people = "Alex";
var years = 42;
console.log("%s is %d years old.", people, years);
```

##### 1.2 console.info
>在控制台打印提示信息
##### 1.3 console.error
>在控制台打印错误信息
##### 1.4 console.warn
>在控制台打印警告信息
##### 1.5 console.clear
>清屏（清空控制台所有信息）
##### 1.6 console.debug
>跟console.log类似，字体颜色会有不同。具体用法还不清晰


#### 2. 其他
##### 2.1 console.group([组名]) && console.groupCollapsed([组名]) && console.groupEnd
>在控制台打印一组信息。
ps: 
	1. group与groupCollapsed均为分组起始，groupCollapsed默认分组时收起的。
	2. group/groupCollapsed与groupEnd要成对出现，否则在其他分组会被包含进无groupEnd的分组中。

```
eg:
console.group('aaa');
console.log('---------');
console.info('---------');
console.error('---------');
console.groupEnd();
```
##### 2.2 console.assert([表达式], [信息])
>表达式的值为false时，打印信息

```
eg:
var a = 1;
console.assert(a === 2, 'a的值出错');
```

##### 2.3 console.count([信息]) 
>统计代码的被执行次数（次数会被追加到信息后）

##### 2.4 console.dir([obj])
>打印出一个对象的结构，方便查看对象

##### 2.5 console.dirxml([DOM ele])
>打印出一个DOM对象所包含的XML/HTML代码

##### 2.6 console.time([标识]) && console.timeEnd([标识]);
>统计一段程序的执行时间
ps:console.time([标识])和console.timeEnd([标识])中方法的标识要相同才能统计出时间。

##### 2.7 console.table([对象数组])
>将数组中的对象以表格形式打印出来

##### 2.8 console.profile([标识]) && console.profileEnd([标识])
>查看CPU的一些信息,可用作性能分析
ps:方法的标识要相同

##### 2.9 console.trace()
>追踪函数的调用轨迹
##### 2.9 console.timeStamp
>用于标记运行时的timeline信息。具体用法还不清楚

#### 3 控制台内置命令行
##### 3.1 keys([obj]) && values([obj])
>打印出一个对象的所有键/所有值
##### 3.2 dir([obj])
>同console.dir
##### 3.3 dirxml([obj])
>同console.dirxml
##### 3.4 clear
>同console.clear

#### 附
>console.timeline 同console.time
console.timelineEnd 同console.timeEnd
console.markTimeline 同console.timeStamp