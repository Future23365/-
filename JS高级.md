# JS高级

## 1 类

### 1.1创建类

~~~ javascript
class Name {
    
}
~~~

### 1.2 类 constructor 构造函数

~~~ javascript
class Name {
    constructor() {		//构造函数
        
    }
}
~~~

### 1.3 类中方法

不用加function()

类里面调用不加小括号

### 1.4 继承

extends

super可以调用父类的构造函数super()，也可以调用父类的方法super.say()

1. 继承中，如果实例化子类输出一个方法，先看子类有没有这个方法，如果有就先执行子类的
2. 如果子类没有，就去查找父类有没有这给方法，如果有，就执行父类的这个方法（就近原则）

super必须放到子类this之前

### 1.5 使用类的注意事项

1. 在ES6中类没有变量提升，所以必须先定义类，才能通过类实例化对象
2. 类里面的共有属性和方法一定要加this使用
3. constructor里面的this指向实例对象，方法里面的this指向这个方法的调用者

## 2 构造函数和原型

实例成员： 是构造函数内部通过this添加的成员

实例成员只能通过实例化的对象来访问

静态成员：在构造函数本身上添加的成员

静态成员只能通过构造函数来访问

### 2.1 构造函数原型 prototype

javascript规定，每一个构造函数都有一个prototype属性，指向另一个对象，

我们可以把那些不变的方法，直接定义在prototype对象上，这样所有的对象的实例都可以共享这些方法

~~~ javascript
Star.protptype.sing=function() {
    
}
~~~

### 2.2 对象原型\__proto__

对象都会有一个属性\__proto__指向构造函数的prototype原型对象

### 2.3 原型constructor 构造函数

对象原型（\__proto__）和构造函数原型对象（prototype）里面都要一个constructor属性，它指回原来的构造函数

如果我们修改了原型对象，给原型对象赋值是一个对象，则必须手动的利用constructor指回原来的构造函数

### 2.4 原型链

![image-20200401205625793](.\image\原型链.png)

### 2.5 JavaScript的成员查找机制

① 当访问一个对象属性（包括方法）时，首先， 查找这个对象自身有没有该属性

② 如果没有就查找它的原型（也就是\__proto__指向的prototype原型对象）

③ 如果还没有就查找原型对象的原型（Object的原型对象）

④ 以此类推一直找到Object为止（null）

### 2.6 原型对象里的this

原型对象函数里面的this指向的是实例对象

### 2.7 扩展内置对象

### 2.8 call()方法

~~~ javascript
fun.call(thisArg, arg1, arg2, ...)
~~~

- thisArg:当前调用函数this的指向对象
- arg1,arg2： 传递的其他参数

例子：

1 可以调用函数

~~~ javascript
fh.call()
~~~

2 可以改变这个函数的this指向

~~~ javascript
fn.call(o)			//这个函数的this就指向了o
~~~

### 2.9 利用父构造函数继承属性

用call（）方法把父类的this指向子类的this

#### 2.10 利用原型对象继承方法

![](G:\html\笔记\image\利用原型对象继承父方法.png)

***如果利用对象的形式修改了原型对象，别忘了利用constructor指回原来的构造函数***

## 3 类的本质

1. 类的本质还是个函数 我们可以简单的认为类就是构造函数的另一种写法
2. 类的所有方法都定义在类的prototype属性上
3. 类创建的实例，里面也有\__proto__指向类的prototype原型对象
4. 所以ES6类的绝大部分功能ES5都可以做到，ES6的类其实就是语法糖

## 4 ES5中新增方法

### 4.1 数组方法

迭代（遍历）方法： forEach(), map(), filter(), sone(), every();

~~~ javascript
array.forEach(function(currentValue, index, arr))
~~~

- currentValue: 数组当前项的值
- index: 数组当前项的索引
- arr: 数组对象本身

~~~ javascript
array.filter(function(currentValue, index, arr))
~~~

- filter() 方法用于创建一个新的数组，新数组中的元素是通过检查指定数组中符合条件的所有元素，主要用于筛选数组
- 注意它直接返回一个新数组

~~~ javascript
array.some(function(currentValue, index, arr))
~~~

- some()方法用于检测数组中的元素是否满足指定条件，
- 注意它返回值是布尔值，如果查找到这个元素，就返回true，否则返回false
- 如果找到第一个满足条件的元素，则终止循环，不在继续查找

### 4.2forEach 和 some 的区别

forEach 里面的return不会终止迭代 

在some里 遇到 return true就会终止迭代，效率高

### 4.3字符串方法

trim() 方法会从一个字符串的两端删除空白字符

~~~ javascript
str.trim()
~~~

trim() 方法不会影响原字符串本身，它返回的是一个新的字符串

### 4.4 对象方法

1 Object.defineProperty() 定义对象中新属性或修改原有属性

~~~ javascript
Object.defineProperty(obj, prop, descriptor)
~~~

- obj: 必需。目标对象
- prop: 必需。需定义或修改的属性的名字
- descriptor: 必需。目标属性所拥有的特征

第三个参数descriptor说明： 以对象形式{}书写

- value: 设置属性的值。默认为undefined
- writable: 值是否可以重写。 true|false 默认为false
- enumerable: 目标属性是否可以被枚举。 true|false 默认为false
- configurable: 目标属性是否可以被删除或是否可以再次修改特征 true| false 默认为false

2 Object.keys()用于获取对象自身所有的属性

~~~ javascript
Object.keys(obj)
~~~

- 效果类似 for...in
- 返回一个由属性名组成的数组

## 5 函数进阶

### 5.1 函数定义方式

第三种定义方式： new function(’参数1‘, ’参数二‘, ’函数体‘)

所有函数都是Function的实例（对象）

函数也属于对象

### 5.2 函数内 this 的指向

| 调用方式     | this指向                                  |
| ------------ | ----------------------------------------- |
| 普通函数调用 | window                                    |
| 构造函数调用 | 实例对象 原型对象里面的方法也指向实例对象 |
| 对象方法调用 | 该方法所属对象                            |
| 事件绑定调用 | 绑定事件对象                              |
| 定时器函数   | window                                    |
| 立即执行函数 | window                                    |

### 5.3 改变函数内部指向

#### 5.3.1 call()方法

#### 5.3.2 apply 方法

~~~ javascript
fun.apply(thisArg, [argsArray])
~~~

- thisArg: 在fun函数运行时指定this值
- argsArray: 传递的值，必须包含在数组里面
- 返回值就是函数的返回值，因为它就是调用函数

应用：可以利用 apply 借助于数学内置对象求最大值

Math.max.apply(null,arr);

#### 5.3.3 bind方法

bind()方法不会调用函数，但是能改变函数内部this指向

~~~ javascript
fun.bind(thisArg, arg1, arg2, ...)
~~~

- thisArg: 在fun函数运行时指定的this值
- arg1, arg2:传递的其他参数
- 返回由指定的this值和初始化参数改造的原函数拷贝

应用： 如果有的函数我们不需要立即调用，但是又想改变这个函数内部的this指向，此时用bind

### 5.4 严格模式

1. 消除了javascript语法的一些不合理、不严谨之处，减少了一些怪异行为
2. 消除代码运行的一些不安全之处，保证代码运行的安全
3. 提高编译效率，增加运行速度
4. 禁用了ECMAScript在未来版本中可能定义的语法

#### 5.4.1 为脚本开启严格模式

使用'use strict'

#### 5.4.2 为某个函数开启严格模式

在函数里面使用‘use srtict’

#### 5.4.3 严格模式的变化

##### 5.4.4 变量规定

1. 必须赋值
2. 严禁删除已经声明变量

##### 5.4.5 this指向问题

在严格模式下全局作用域中函数中的this是underfined

##### 5.4.6 函数变化

1. 函数不能有重名的参数

### 5.5 高阶函数

高阶函数是对其他函数进行操作的函数，它**接收函数作为参数**或**将函数作为返回值输出**

## 6 闭包

闭包指有权访问另一个函数作用域中变量的函数

**主要作用：** 延伸了变量的作用范围

## 7 正则表达式

### 7.1 创建正则表达式

#### 7.1.1 通过RegExp对象的构造函数创建

~~~ javascript
var 变量名 = new RegExp(/表达式/);
~~~

#### 7.1.2 通过字面量创建

~~~ javascript
var 变量名 = /表达式/;
~~~

#### 7.1.3 测试正则表达式 test

test() 用于检测字符串是否符合该规则，该对象返回true或false

~~~ javascript
regexObj.test(str)
~~~

1. regexobj是写的正则表达式
2. str 我们要测试的文本
3. 所用：检测str文本是否符合我们写的正则表达式规范

#### 7.1.4 边界符

| 边界符 | 说明                           |
| ------ | ------------------------------ |
| ^      | 表示匹配行首的文本（以谁开始） |
| $      | 表示匹配行尾的文本（以谁结束） |

#### 7.1.5 字符类

[]匹配其中一个

[-]方括号内部范围符

如果中括号里面有^表示取反

#### 7.1.6 量词符

| 量词  | 说明            |
| ----- | --------------- |
| *     | 重复零或多次    |
| +     | 重复一次或多次  |
| ?     | 重复零次或一次  |
| {n}   | 重复n次         |
| {n,}  | 重复n次或更多次 |
| {n,m} | 重复n到m次      |

#### 7.1.7 预定义类

| 预定义类 | 说明          |
| -------- | ------------- |
| \d       | 相当于[0-9]   |
| \D       | [^0-9]        |
| \w       | [a-zA-Z0-9]   |
| \W       | [^A-Za-z0-9]  |
| \s       | [\t\r\n\v\f]  |
| \S       | [^\t\r\n\v\f] |

### 7.2 replace替换

replace()方法可以实现替换字符串操作，用来替换的参数可以是一个字符串或是一个正则表达式

~~~ javascript
stringObject.replace(regexp/substr,replacement)
~~~

1. 第一个参数：被替换的字符串或者正则表达式
2. 第二个参数：替换为字符串
3. 返回值是一个替换完毕的新字符串

### 7.3 正则表达式从参数

~~~ javascript
/表达式/[switch]
~~~

switch(也称为修饰符)按照什么样的模式来匹配，有三种值

- g：全局匹配
- i: 忽略大小写
- gi: 全局匹配+忽略大小写

## 8 ES6

### 8.1 let

- let声明的变量只在所处于的块级有效
- 不存在变量提升
- 暂时性死区

### 8.2 const

声明常量，常量就是值（内存地址）不能改变

- 具有块级作用域
- 声明常量时必须赋值
- 常量赋值后，值不能修改
  - 对于基本数据类型：值不能更改
  - 对于复杂数据类型：值可以改，地址不能改

### 8.3 解构赋值

**数组解构**

例子：

~~~ javascript
let ary = [1,2,3];
let [a,b,c] = ary;			//a,b,c变量就存了数组的值
~~~

**对象解构**

例子：

~~~ javascript
let person = {name:'vahgj', age: 20}
let {name,age} = person;			//name,age就存了属性的值
~~~

另一种方式：

~~~ javascript
let {name: myName} = person			//myName为自己定义的变量
~~~

### 8.4 箭头函数

~~~ javascript
() => {}
const fn = () => {}
~~~

1. 函数体只有一句代码，且代码的执行结果就是返回值，可以省略大括号
2. 如果形参只有一个，可以省略小括号

#### 8.4.1 箭头函数this

箭头函数不绑定this关键字，箭头函数中的this，指向的是函数定义位置的上下文this

### 9 剩余参数

~~~ javascript
function sum (first, ...args) {
    console.log(first);//10
    console.log(args);//[20,30]
}
sum(10,20,30)
~~~

