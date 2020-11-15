# 一、 初识JavaScript

## 1.1 JS的组成

- ECMAScript  javascript语法
- DOM 页面文档对象模型
- BOM 浏览器对象模型

## 1.2 JS输入输出

- 输入框 prompt()
- 弹出框 alert()
- 控制台输出 console()

## 1.3 JS变量

JavaScript是一种弱类型或者说是动态语言

不用var 定义的变量属于全局变量

## 1.4 数据类型

- 简单数据类型
- 复杂数据类型

字符串建议单引号

typeof 检测数据类型

~~~ javascript
typeof num
~~~

### 1.4.1 数据类型行转换

###### 转换为字符串： 

1. toString()
2. String()强制转换

###### 转换为数字：

1. parselnt(string)
2. ParseFloat(string)
3. Number() 强制转换
4. JS隐式转换

###### 转换为布尔型

Boolean()

**浮点数不能作为比较**

## 1.5 数组

- 可以通过修改数组长度修改数组大小
- 可以通过修改索引号的方式修改数组大小
- instanceof 可以检测是否为数组

##### 添加元素

数组.push()     push完毕后返回的是新数组的长度

数组.unshift() 在数组前面添加元素

##### 删除元素

pop() 返回删除的元素

shift() 删除第一的元素

##### 冒泡排序

~~~ javascript
arr.sort(function(a,b){
    return  a - b //升序
})
~~~

##### 获取索引

- indeOf() 数组中给定元素的第一个索引
- lastIndexOf()在数组中的最后一个索引

##### 转换为字符串

- toString() 把数组转换成字符串，逗号分隔每一项
- join('分隔符') 把数组中的所有元素转换为一个字符串



## 1.6 函数

~~~ javasc
function sum() {

}
~~~



形参和实参可以不相等

arguments可以获取实参，它里面存储了实参，

**es6才有块级作用域**

## 1.7 预解析

JS引擎会把js里面所有的**var**，**function**提升到当前作用域的最前面

##### 1.7.1变量预解析

把所有的变量声明提升到当前作用域最前面 不提升赋值操作

##### 1.7.2 函数提升

把所有的函数声明提升到当前作用域的最前面 不调用函数

## 1.8 对象

### 1.8.1 对象的创建

#### 1.8.1.1 利用字面量创建对象

~~~ javascript
var obj = {
    uname: '张三丰',
    sex: '男',
    sayHI: function() {
        console.log('hi~');
    }
}
~~~

1. 属性或方法采用键值对的形式
2. 多个属性或方法中间用逗号隔开
3. 方法冒号后面跟的是一个匿名函数

调用属性的另一种方法：

~~~ javascript
obj['uname']
~~~

#### 1.8.1.2 利用new Object创建对象

~~~ javascript
var obj = new Object();
obj.uname = '张三丰';
obj.age = 18;
obj.sex = '男';
obj.sayHi = function() {
    console.log('Hi~')
}
~~~

#### 1.8.1.3 利用构造函数创建对象

~~~ javascript
function 构造函数名（） {
    this.属性 = 值;
    this.方法 = function() {}
}
new 构造函数名();
~~~

**约定 ：构造函数首字母大写**

遍历对象：

~~~ javascript
for (变量 in 对象) {
    console.log(变量) // 变量输出的是属性名
    console.log(对象[变量]) // 输出属性名的值
}
~~~

## 1.9字符串对象

**根据位置返回字符**

| 方法名            | 说明                                       | 使用                       |
| ----------------- | ------------------------------------------ | -------------------------- |
| charAt(index)     | 返回指定位置的字符（index字符串的索引号）  | str.charAt(0)              |
| charCodeAt(index) | 获取指定位置处字符的ASCII码（index索引号） | str.charCodeAt(0)          |
| str[index]        | 获取指定位置处字符                         | HTML5 支持和charAt（等效） |

**拼接及截取字符串**

| 方法名                    | 说明                                                     |
| ------------------------- | -------------------------------------------------------- |
| concat(str1,str2,str3...) | count()方法用于连接两个或多个字符串，拼接字符串，等效于+ |
| substr(start,length)      | 从start位置开始（索引号）开始，length个数，重点          |
| slice(start,end)          | 从 start开始到end，不包括end                             |
| substring(start,end)      | 从strat到end，不包括end不接受负数                        |

**替换字符串**

replace（‘替换前字符’，‘替换后字符’）

**转换为数组**

split（‘分隔符’）