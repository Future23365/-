#  jQuery 

## 1.1 jQueury基本使用

### 1.1.1 jQuery入口函数

~~~ javascript
$(function() {
   ... //此处是页面加载完成的入口
})
~~~

或

~~~ javascript
$(document.ready(function() {
   ... //此处是页面DOM加载完成的入口
}))
~~~

相当于原生js的DOMContentLoaded

### 1.1.2 jQuery 的顶级对象$

### 1.1.3 jQuery 对象和DOM对象

1. 用原生js获取过来的对象
2. 用jQuery获取的对象
3. jQuery对象的本质是：利用$对DOM对象包装后产生的对象（伪数组形式存储）

DOM对象转换为jQuery对象：$（DOM对象）

jQuery对象转换为DOM对象：

~~~ javascript
$('div')[index]		index是索引号
~~~

~~~ javascript
$('div').get[index]		index是索引号
~~~

## 2 jquery常用API

### 2.1 jQuery基础选择器

~~~ javascript
$("选择器") //里面选择器直接写CSS选择器即可，但是要加引号
~~~

| 名称       | 用法            | 描述                  |
| ---------- | --------------- | --------------------- |
| ID选择器   | $('#id')        | 获取指定ID的元素      |
| 全选择器   | $('*')          | 匹配所有元素          |
| 类选择器   | $('.class')     | 获取同一类class的元素 |
| 标签选择器 | $('div')        | 获取同一标签的元素    |
| 并集选择器 | $('div,p,li')   | 获取多个元素          |
| 交集选择器 | $('li.current') | 交集元素              |

### 2.2 jQuery层级选择器

### 2.3 jQuery设置属性

~~~ javascript
$('div').css('属性','值')
~~~

### 2.4 隐式迭代

遍历内部DOM元素（伪数组形式存储）的过程叫做隐式迭代

### 2.5 jQuery筛选选择器

| 语法       | 用法          | 描述                                     |
| ---------- | ------------- | ---------------------------------------- |
| :first     | $('li:first') | 获取第一个li元素                         |
| :last      | $('li:last')  | 获取最后一个li元素                       |
| :eq(index) | $('li:eq(2)') | 获取到的li元素中，选择索引号为2的元素    |
| :odd       | $('li:odd')   | 获取到的li元素中，选择索引号为奇数的元素 |
| :even      | $('li:even')  | 获取到的li元素中，选择索引号为偶数的元素 |

| 语法               | 用法                           | 说明                                                   |
| ------------------ | ------------------------------ | ------------------------------------------------------ |
| parent()           | $('li').parent();              | 查找父级                                               |
| children(selector) | $('ul').children();            | 相当于$('ul>li'),最近一级（亲儿子）                    |
| find(selector)     | $('ul').find('li');            | 相当于$('ul li'),后代选择器                            |
| siblings(selector) | $('.first').sibling('li');     | 查找兄弟节点，不包括自己本身                           |
| nextAll([expr])    | $('.first').nextAll()          | 查找当前元素之后所有的同辈元素                         |
| prevtAll([expr])   | $('.ladt').prevAll()           | 查找当前元素之前的所有同辈元素                         |
| hasClass(class)    | $('div').hasclass('protected') | 检查当前的元素是否含有某个特定的类，如果有，则返回true |
| eq(index)          | $('li').eq(2)                  | 相当于$('li:eq(2)'),                                   |

### 2.6 链式编程

~~~ javascript
$(this).css('color','red').siblings().css('color','');
~~~

## 3 jQuery样式操作

### 3.1 操作CSS方法

1.参数只写属性名，则是返回属性值

~~~ javascript
$(this).css('color');
~~~

2.参数是属性名，属性值，逗号分隔，是设置一组样式，属性必须加引号，值如果是数字可以不用跟单位和引号

~~~ javascript
$(this).css('color', 'red');
~~~

3.参数可以是对象形式，方便设置多组样式。属性名和属性值用冒号隔开，属性可以不用加引号

~~~ javadscript
$(this).css({
'color':white,
'font-size':20px
});
~~~

### 3.2 设置类名方法

1.添加类

~~~ javascript
$('div').addClass('current');
~~~

2.删除类

~~~ javascript
$('div').removeClass('current');
~~~

3.切换类

~~~ javascript
$('div').toggleClass('current');
~~~

## 4 jQuery 效果

### 4.1 显示与隐藏

**显示，隐藏,切换,下滑，上划，切换**：

~~~ javascript
show([speed,[easing],[fn]]);		//显示
hide([speed,[easing],[fn]]);		//隐藏
toggle([speed,[easing],[fn]]);		//切换
slideDown([speed,[easing],[fn]]);	//下划
slideUp([speed,[easing],[fn]]);		//上划
slideToggle([speed,[easing],[fn]]);	//切换
~~~

1. 参数都可以省略，无动画直接显示
2. speed：三种预定义速度之一的字符串（“show”,"normal","fast")或表示动画时长的毫秒数
3. easing：用来指定切换效果，默认是“swing”，可用参数“linear”
4. fn：回调函数，在动画完成时执行的函数，每个元素执行一次

### 4.2 事件切换

~~~ javascript
hover([over,]out)
~~~

1. over:鼠标移动到元素上要触发的函数（相当于mouseenter)
2. out:鼠标移出元素要触发的函数（相当于mouseleave)

### 4.3 动画队列及其停止排队方法

**停止排队**：

~~~ javascript
stop()		//结束上一个动画
~~~

#### 4.4 淡入淡出效果

**淡入,淡出，切换**

~~~ javascript
fadeIn([speed,[easing],[fn]])		//淡入
fadeOut([speed,[easing],[fn]])		//淡出
fadeToggle([speed,[easing],[fn]])	//切换
~~~

渐进方式调整到指定的不透明度

~~~ javascript
fadeTo([[speed],opacity,[easing],[fn]])
~~~

1. opacity透明度必须写，取值0~1之间
2. speed:必须写

### 4.5 自定义动画

~~~ javascript
animate(params,[speed],[easing],[fn])
~~~

1. params:想要更改的样式属性，以对象的形式传递，必须写。属性名可以不用带引号，如果是复合属性则需要采取驼峰命名法borderLeft，其余参数可以省略

## 5 jQuery属性操作

### 5.1 设置或获取元素固有属性值 prop()

**获取属性值：**

~~~ javascript
prop('属性')
~~~

**设置属性值**

~~~ javascript
prop('属性','属性值')
~~~

### 5.2 设置或获取元素自定义属性值 attr()

~~~ javascript
attr("属性")		//类似原生getAttribute()
attr("属性","属性值")//类似原生setAttribute()
~~~

### 5.3 数据缓存 data()

## 6 内容文本值

### 6.1 普通元素内容html() (相当于原生innerHTML)

~~~ javascript
html()		//获取元素内容
html("内容")	//设置元素内容
~~~

### 6.2 普通文本内容 text() (相当于原生innerText)

~~~ javascript
text()			//获取元素文本内容
text("文本内容") //设置元素的文本内容
~~~

### 6.3 表单的值val() (相当于原生value)

~~~ javascript
val()
val("文本内容")
~~~

## 7 jQuery元素操作

### 7.1 遍历元素

~~~ javascript
$("div").each(function (index, domEle) { xxx; })
~~~

1. index是每个元素的索引号，demELe是每个DOM元素对象，不是jQuery对象
2. 所以想要使用jQuery方法，需要给这个dom元素转换为jQuery对象$(domEle)

~~~ javascript
$.each(object, function(index,element) { xxx; })
~~~

1. $.each()方法可用于遍历任何对象，主要用于数据处理，比如数组，对象
2. 参数： index是每个元素的索引号，element 遍历内容

### 7.2 创建元素

~~~ javascript
$("<div></div>");
~~~

### 7.3 添加元素

#### 7.3.1 内部添加

~~~ javascript
element.append("内容");		//把元素放入匹配元素内部的后面，类似原生appendChild
element.prepend("内容")		//把元素放入匹配元素内部的前面
~~~

#### 7.3.2 外部添加

~~~ javascript
element.after("内容");		//把内容添加到目标元素的后面
element.before("内容");		//把内容添加到目标元素的前面
~~~

#### 7.4 删除元素

~~~ javascript
element.remove()		//删除匹配的元素（本身）
element.empty()			//删除匹配的元素集合中所有的子节点
element.html("")		//清空匹配的元素内容
~~~

## 8 jQuery尺寸、位置操作

### 8.1 jQuery尺寸

| 语法                               | 用法                                                 |
| ---------------------------------- | ---------------------------------------------------- |
| width()/height()                   | 取得匹配元素宽度和高度 只算width/height              |
| innerWidth()/innerHeight()         | 取得匹配元素宽的和高度值 包含padding                 |
| outerWidth()/outerHeight()         | 取得匹配元素宽度和高度值 包含padding、border         |
| outerWidth(true)/outerHeight(true) | 取得匹配元素宽度和高度值 包含padding、border、margin |

- 以上参数为空，则是获取相应值，返回的是数字型
- 如果参数为数字，则是修改相应值
- 参数可以不写单位

### 8.2 jQuery位置

#### 8.2.1 offset设置或获取元素偏移

1. offset()方法设置或返回被选元素相对于文档的偏移坐标，跟父级没有关系
2. offset（{top：100xp;left：100px}）

#### 8.2.2 position()获取元素偏移

1. position()方法用于返回被选元素相对于带有定位的父级偏移坐标，如果父级都没有定位，则以文档为准

#### 8.2.3 scrollTop()/scrollLeft()设置或获取元素被卷去的头部和左侧

## 9 jQuery事件

### 9.1 jQuery事件注册

**单个事件注册**

~~~ javascript
$("div").click(function() {
    事件处理程序
})
~~~

其他事件和原生基本一致

比如mouseover,mouseout,blur,focus,change,keydown,keyup,resize,scroll等

### 8.2 事件处理 on() 绑定事件

~~~ javascript
element.on(event, [selector], fn)
~~~

1. events: 一个或多个用空格分隔的事件类型，如"click"或"keydown"
2. selector:元素的子元素选择器
3. fn:回调函数，即绑定在元素身上的监听函数

**优势**：

1. 可以注册多个事件
2. 事件委托
3. **给动态创建的元素绑定事件**

### 8.3 事件处理 off() 解绑事件

~~~ javascript
$("p").off()				//解绑p元素所有事件处理程序
$("p").off("click")			//解绑p元素上面的点击事件 foo是监听函数名
$("ul").off("click", "li")	//解绑事件委托
~~~

有的事件只想触发一次，可以使用one()来绑定

### 8.4 自动触发事件 trigger()

~~~ javascript
element.click();			//第一种形式
element.trigger("type")		//第二种自动触发形式
element.triggerHandler(type)//第三种自动触发模式(不会触发元素的默认行为)
~~~

### 8.5 jQuery事件对象

~~~ javascript
element.on(events,[selector],function(event) {})
~~~

## 9 jQuery其他方法

### 9.1 jQuery对象拷贝

~~~ javascript
$.extend([deep], target, object, [objectN])
~~~

1. deep: 如果设为true为深拷贝，默认为false 浅拷贝
2. target: 要拷贝的目标对象
3. object: 待拷贝到第一个对象的对象
4. objectN:待拷贝到的N个对象的对象
5. 浅拷贝是吧被拷贝的对象复杂数据类型中的地址拷贝给目标对象，修改目标对象会影响被拷贝的对象

### 9.2 jQuery 多库共存

noConflict()  可以更改$标识符或jQuery

### 9.3 jQuery插件

jQuery库

#### 9.3.2 图片懒加载

当我们页面滑动到可视区域，再显示图片

#### 9.3.3 全屏滚动插件

https://www.dowebok.com/demo/2014/77/

#### 9.3.4 bootstrap js插件

## 其他

~~~ javascript
JOSN.stringify()			//把数组转换为字符串
JSON.parse()				//把字符串转换为数组
数组.splice(从哪个位置开始删除,删除几个元素)
~~~



