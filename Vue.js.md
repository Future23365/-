# Vue.js

### 1. 创建Vue实例传入的options

- el
  - 类型：string|HTMLElement
  - 作用：决定之后Vue实例会管理哪个DOM
- data
  - 类型：Object|Function(组件当中data必须是一个函数)
  - 作用：Vue实例对象的数据对象
- methods
  - 类型：{[key:string]:Function}
  - 作用：定义属性属于Vue的一些方法，可以在其他地方调用，也可以在指令中使用

### 2 差值操作-指令

#### mustache语法

#### v-once 指令

- 该指令后面不需要跟任何表达式
- 该指令表示元素和组件值渲染一次，不会随着数据的改变而改变

#### v-html

- 该指令后面往往会跟上一个string类型
- 会将string的html解析出来并进行渲染

#### v-text

- 和Mustache比较相似：都是用于将数据显示在界面中
- 通常情况下，接受一个string类型

#### v-pre

- 用于跳过这个元素和它子元素的编译过程，显示原本的Mustanche语法

#### v-cloak

- 在vue解析之前此属性会存在，在vue解析之后此属性会消失，可以搭配css使用

### 3 v-band 动态绑定属性

#### 3.1 基本使用

使用方法：

在属性前面加上： v-band:     属性里面使用变量

简写形式 ： ：

#### 3.2 v-bind绑定class

##### 3.2.1 对象语法绑定

**用法一：**直接通过{}绑定一个类

~~~ css
<h2 :class="{'active': isActive}">Hello world</h2>
~~~

**用法二：**可也以用过判断，传入多个值

~~~ css
<h2 :class="{'active': isActive, 'line': isLine}">Hello world</h2>
~~~

**用法三：**和普通的类同时存在，并不冲突

~~~ css
<h2 class="title" :class="{'active': isActive, 'line': isLine}">Hello world</h2>
~~~

**用法四：**如果过于负载，可以放在一个methods或者computer中(classes是一个计算属性)

~~~ css
<h2 class="title" :class="classes">Hello world</h2>
~~~

##### 3.2.2 数组语法绑定

class后面跟的是一个数组，数组里面存类名，用法同对象语法但没有boolean

#### 4 v-bind 绑定style

##### 4.1 对象语法绑定

style后面跟的是一个对象名称

- 对象的key是CSS属性的名称
- 对象的value是具体赋的值，值可以来自于data炸的属性

##### 4.2 数组语法绑定

style后面跟的是一个数组类型（数组里面存的是变量（这个变量里面存的是数组））

- 多个值以“，”分隔即可

#### 5 计算属性

写在 实例的cpmputed 选项中

计算属性会进行缓存，多次使用时，计算属性只会调用一次，提高性能

- 每一个计算属性都包含一个getter和一个setter
  - 经常使用get来读取
  - 有些时候使用set方法（更改属性的值会回调set方法）

### 6 事件监听 v-on 

简写形式：@

参数：

- 如果该方法不需要额外的参数，那么方法后的（）可以不添加
  - 如果方法本身中有一个参数，但没写括号，那么会默认将原生事件event参数传递进去
- 如果需要同时传入某个参数，可以通过$event传入事件

#### 6.1 v-on 修饰符

- .stop 调用event.stopPropagation();				//阻止事件冒泡
- .prevent 调用event.preventDefault();            //阻止默认事件
- .{keyCode|keyAliax} 只当事件是从特定键触发时才触发回调                  //.enter就是按enter键才触发
- .native 监听组件根元素的原生事件
- .once 只触发一次回调

### 7 v-if v-else-if v-else

#### 7.1 v-if

- true显示
- false不显示

#### 7.2 v-else

和v-if搭配 v-if不显示时v-else显示

#### 7.3 v-else-if

类似if else

#### 小提示 :sweat_smile:

vue在渲染界面是可能会出现复用组件的情况(组件没有变，只是属性的值变了)，可以加上key标识来解决这个问题

#### 7.4 v-show

和v-if的区别

- v-if 当条件为false时，压根不会有对应的元素在DOM中
- v-show当条件为false时，仅仅是将元素的display属性设置为none而已

开发中的选择：

- 当需要显示与隐藏之间切换很频繁时，使用v-show
- 当只有一次切换时，使用v-if

### 8 v-for

#### 8.1 遍历数组

~~~ vue
v-for="item in movies"
v-for="(item index) in movies"			//index为索引号
~~~

#### 8.2 遍历对象

~~~ vue
v-for="item in info" //如果只是获取一个值，那么获取到的是value
v-for="(value key) in info"	//获取key和value
v-for="(value key index) in info"	//获取key、value和index
~~~

#### 8.3 组件的key属性

### 9 数组中的响应式方法

#### 9.1 响应式方法

- push() //在数组后面添加元素
- pop()  //删除数组最后一个元素
- shif()  //删除数组第一个元素
- unshift() //在数组第一个元素前面添加元素
- splice()  //可以传入三个参数，第一个参数为开始的索引号，第二个参数删除元素的个数，第三个参数为添加的元素，可以添加多个元素（只传一个参数为从当前索引号删除元素到最后，不传参数为删除所有元素）
- sort()   //数组排序
- reverse()   //数组反转

#### 9.2 非响应式方法

- 通过索引值修改数组中的元素

#### 10 过滤器

写在filters里面，类似一个函数

调用时在属性后面加上 | 过滤器名称

例：

~~~ javascript
item.price | 过滤器名称
~~~

### 知识回顾

##### 高阶函数：

filter ：回调函数有一个要求，必须返回一个boolean值，当返回为true时，函数内部会自动调用这次回调的n加入到新的数组中，当返回为false时，函数内部会过滤掉这次的n

map：返回数组中每一个数

reduce： 传两个参数，对数组中所有内容进行汇总

### 11 v-model 双向绑定

单选框对应boolean值，多选框对应数组

#### 11.2 值绑定

~~~ html
<label v-for="item in originHobbies" :for="item">
	<input type="checkbox" :value="item" :id="item" v-model="hobbies">{{item}}
</label>
~~~

#### 11.3 修饰符

- lazy修饰符
  - 可以让数据在失去焦点时或者按回车才会更新
- number修饰符
  - 可以让输入框中输入的内容自动转成数字类型
- trim修饰符
  - 可以过滤内容左右两边的空格

### 12 组件化

#### 12.1 注册组件的基本步骤

**1 创建组件构造器**

~~~ javascript
const 组件构造器名字 = Vue.extend({
    template: ...				//组件内容
})
~~~

**2 注册组件**

~~~ javascript
Vue.component('组件名字'，组件构造器名字 )
~~~

**3 使用组件**

~~~ javascript
<组件名字></组件名字>
~~~

***4语法糖写法（vue2.几之后的写法）***

不需要单独用extend创建构造器（局部和全局都可以省略）

~~~ javascript
Vue.component('cpu', {			//组件名字
	template: `			//``为es6新增字符串的写法
		...         //组件内容
	`
})
~~~



#### 12.2 局部组件与全局组件

在Vue实例里面注册的组件（第二步的注册组件）是局部组件

#### 12.3 z父组件和子组件

在父组件里注册并使用子组件

#### 12.4 组件模板分离写法

##### 12.4.1 使用\<sctipt>\</script>标签

~~~ javascript
<script type="text/x-template" id="myCpn">	//type为固定形式，id为注册组件构造器名字
    ...			//组件内容
</script>
~~~

##### 12.4.2 使用 template 标签

~~~ javascript
<template id="cpn">			//id效果同上
	...		//组件内容
</template>
~~~

##### 12.5 组件访问数据

组件不能访问vue实例中的data数据

可以在注册组件的data中写入数据，但是不是对象的格式，而是使用函数形式(因为对象会共用一个地址，会相互影响，函数返回的对象则不会)

~~~ javascript
Vue.component('cpn', {
    template: '#cpn',
    data() {
        return {
            title: 'abc'			//数据内容
        }
    }
})
~~~

##### 12.6 父子组件的通讯

**1 通过props向子组件传递数据**

- 字符串数组，数组中的字符串就是传递时的名称

~~~ javascript
const cpn = {
  template: '#cpn',
  props: ['cmovies'],			//这里的comvies就是父组件data中的键值对的名称
  data() {
    return {
    }
  }
}
~~~

另一种写法：**（经常使用）**​

~~~ javascript
props: {
    cmovies: Array,			//前边为父组件定义数据的名称，后变为数据类型
  }
还可以提供一些参数：
props: {
        cmovies: Array,
        cmessage: {
            type: String,		//类型
            default:'aaaaaa'	//默认值
            ...					
        }
    }
~~~



- 对象，对象可以设置传递时的类型，也可以设置默认值等

***注意事项***::smiley_cat:

1. props里面的变量名（上边的cmovies, cmessage）不可以使用驼峰命名法，不然在使用组件时会出现错误(驼峰命名法的话在大写字母前面加上-，如c-move)，原因html属性不区分大小写
2. 定义组件模板时要有根节点，比如在根节点套一个div，不然会报错

**2 通过事件向父组件发送消息**

1. 子组件在事件里发送事件（事件类型自定义）

~~~ javascript
btnClick(item) {
    this.$emit('item-click',传递的参数);		//item-click为自定义的类型
}
~~~

2. 父组件在使用标签的时候用v-on接受事件

~~~ javascript
<cpn @item-click='父组件事件执行函数'></cpn>
~~~

##### 12.7 父子组件的访问方式

- 父组件访问子组件：使用$children或$refs
  - $refs使用方法（常用）
    - 在标签里ref属性里写任意的名即可
    - 使用时用$refs.ref属性里的明子即可
- 子组件访问父组件：使用$parent
- 访问根vue实例：$root

#### 13 插槽(slot)

在组件模板里面加上\<solt>\</solt>即可

如果想要实现大部分组件里有共性，只有少部分没有，则在\<solt>\</solt>里面写上东西，少数没有的修改即可

##### 13.1具名插槽

当使用多个插槽但只想改变其中一个时可以给插槽家name属性，更改时在组件里面声明solt=“插槽name属性的值”即可

例：

~~~ javascript
插槽声明：
<template id="cpn">
    ...
	<solt name="center"></solt>
	...
</template>
插槽使用：
<cpn><button slot="center"></button></cpn>
~~~

***此插槽方法已被废弃，使用时注意看官网***\:smiley:

##### 13.2 作用域插槽

父组件替换插槽的标签，但是内容由子组件来提供

（父组件得到子组件的数据，样式由父组件决定）

方法：

在模板里面增加：自定义名字=“数据属性名”， 在父组件使用子组件时，必须定义template标签，标签里面属性加上slot-scope="slot（***此处可能已经更新，使用时注意看官网***），然后调用加上slot.自定义名字即可

例：

~~~ javascript
父组件调用：
<cpn>
	<template slot-scope="slot">		//template必须写，属性必须加
        <span v-for="item in slot.data"></span>
    	
    </template>
</cpn>

子组件：
components: {
    cpn: {
        template: '#cpn',
         data() {
            return {
			pLanguages: ['','']	//数据
            }
        }
    }
}
~~~

### 14 模块化

#### 14.1 CommonJS

##### 14.1.1 CommonJS的导入

~~~ javascript
module.exports = {
    flat: true,
    test() {
        
    },
    ...
}
~~~

##### 14.1.2 CommonJS的导入

~~~ javascript
let {test, demo, flag} = require('moduleA')
~~~

#### 14.2 ES6的模块化

1. 在script标签里面加上type="model"代表这个js文件是模块化的，这样每个js文件就有一个单独的作用域

2. export导出

   1. 导出方式1

      ~~~ javascript
      export {
      	flag,sum
      }
      ~~~

   2. 导出方式2

      ~~~ javascript
      export var num = 1;
      ~~~

   3. 导出函数/类

      ~~~ javascript
      export function num() {
      }
      export class Person {
      }
      ~~~

3. export default 可以在导入时自定义名字，只能有一个

4. import导入

   ~~~ javascript
   import {} form "js文件位置" //导入export default时不加{}
   ~~~

5. 统一全部导入

   ~~~ javascript
   import * as aaa form "js文件"
   aaa.		//使用从aaa里面调用即可
   ~~~

### 15 webpack 

首先安装node

再用 npm装webpack

~~~ javascript
npm install webpack@3.6.0 -g
~~~

打包在控制台使用webpack打包

**输入webpack自动打包**

1 在目录下创建webpack.config.js文件

2 在里面写入如下内容

~~~ javascript
const path = require('path');
moudle.exports = {
    entry: './src/main.js',		//入口
    output: {
        path: path.resolve(__dirname, 'dist'),			//动态获取出口路径（必须是绝对路径）这里用到了node
        filename: 'bundle.js'	//出口文件名
    }
}
~~~

用到的命令： npm init

可以在生成的package.json文件里面的script里面配置映射：

"build": "webpack"(***这里面定义之后优先使用局部的webpack***)

这用就可以在控制台输入npm run build来进行打包，就不用使用webpack命令了

***建议安装局部webpack开发时依赖***

命令： 

~~~ javascript
npm install webpack@3.6.0 --save-dev
~~~

#### 15.1 loador

可以导入css文件，等等，去webpack官网找即可

导入css还需要导入style-loader使之生效

在webpack.config.js里面加入

**webpack导使用loder时读取user的顺序是从右向左读的**

**图片文件处理**

同上使用loader

当图片小于limit时，会将图片编译成base64字符串的形式

当图片大于limit时，会使用file-loader，所以得安装file-loader

当使用file-loader时，必须在webpack.config.js配置里面的putput里面加入publicPath: 'dist/'（dist为输出目录名）

可以为生成的图片命名，在options里面加上：name: 'img/[name].[hash:8].[ext]'即可，[]为固定写法，ext为后缀

**ES6转ES5工具： babel** 

安装loader：

~~~ javascript
npm install --save-dev babel-loader@7 babel-core babel-preset-es2015
~~~

配置webpack.config.js文件：(这里和官网不太一样)

~~~ javascript
    {
      test: /\.js$/,
      exclude: /(node_modules|bower_components)/,
      use: {
        loader: 'babel-loader',
        options: {
          presets: ['es2015']
        }
      }
    }
~~~

#### 15.2 引入Vue

npm安装vue：

~~~ javascript
npm install vue --save
~~~

导入Vue

~~~ javascript
import Vue from 'vue'
~~~

报错，需要在配置文件里加上：

~~~ javascript
module.exports = {
    ...
    ...
    resolve: {
    alias: {
      'vue$': 'vue/dist/vue.esm.js'
    }
  }
} 

~~~

**el 和 template 区别**

template会替换el绑定的组件

***组件抽离：***

1 配置loader：

~~~ javascript
npm install vue-loader vue-template-compiler --save-dev
~~~

2 配置webpack.config.js:

~~~ javascript
module.exports = {
    ...
    module: {
        rules: {
            ...
            {
                test: /\.vue$/,
                use: ['vue-loader']
            }
        }
    }
}
~~~

3 在package.json中换vue-loader的版本为13.几,重新安装vue-loader

 4 在index中之定义一个\<div id="app">\</div>

![](D:\liusongbai\html\笔记\image\组件化抽取01.PNG)

5 在App.vue中声明组件模板

![](D:\liusongbai\html\笔记\image\组件化抽取02.PNG)

6 在main.js里面导入模板，并注册组件

![](D:\liusongbai\html\笔记\image\组件化抽取03.PNG)

#### 15.3 plugin(插件)

##### 15.3.1 添加版权的pluguin--BannerPlugin

~~~ javascript
const webpack = require('webpack');		//导入

module.exports = {
    ...
    plugins: [
        new webpack.BannerPlugin('版权信息')	//添加版权信息
    ]
}
~~~

##### 15.3.2 打包html的plugin--HtmlWebpackPlugin插件

- 自动生成一个index.html文件（可以指定模板来生成）
- 将打包的js文件，自动通过script标签插入到body中

安装：

~~~ javscript
npm install html-webpack-plugin --save-dev
~~~

使用

首先删除plubicPath: "dist/"

接着在webpack.config.js 文件的pluins部分插入代码：

~~~ javascript
const HtmlWebpackPlugin = require('htnl-webpack-plugin');		//声明

module.exports = {
    ...
    plugins: [
        ...
        new HtmlWebpackPlugin = ({
            template: 'index.html'		//使用并指定模板
        })
    ]
}
~~~

##### 15.3.3 js压缩Plugin--uglifyjs-webpack-plugin

安装：

~~~ javascript
npm install uglifyjs-webpack-plugin@1.1.1 --save-dev
~~~

配置webpack.config.js文件：

~~~ javascript
const uglifyJsPlugin = require('uglifyjs-webpack-plugin');				//声明变量

module.exports = {
    ...
    plugins: [
        ...
        new uglifyJsPlugin()		//调用
    ]
}
~~~

<span style="color:red">高版本可能有的插件不能用或者自带某个插件，请留意,注意官网查询</span>

##### 15.3.4 搭建本地服务器

这个本地服务器给予node.js搭建,内部使用ecpress框架，可以让浏览器自动刷新修改后的结果

安装：

~~~ javascript
npm install --save-dev webpack-dev-server@2.9.1
~~~

设置属性：

- contentBase:
- port:
- inline:
- historyApiFallback:

webpack.config.js配置：

~~~ javascript
devServer: {
    contentBase: './dist',
    inline: true
}
~~~

可以再json里面配置便携写法

~~~ javascript
{
    ...
    "dev": "webpack-dev-server --open"		//--open为自动打开浏览器，可以不写
}
~~~

ctrl +c 终止

<span>webpack有些是开发时的配置，在发布时可能用不到</span>

**webpack配置文件分离**

可以将开发时的依赖和生产时的依赖单独放入一个文件夹，

比如： 公共的放在bsse.config.js里面

开发时的放在dev.config.js里面

生产时的放在prod.config.js里面

r然后需要webpack装插件：

~~~ javascript
npm install webpack-merge --save-dev
~~~

然后的分离的文件里面导入:

~~~ javascript
const webpackMerge = require('webpack-merge')
const baseConfig = require('./base.config')

module.exports = webpackMerge(baseConfig, {
plugins:[
    ...		//生产时插件|开发时插件
]})
    
~~~

然后在package.json里面配置build项：(不然还会默认使用webpack.config.js)

~~~ javascript
{
    ...
    "scripts": {
        ...
        "build": "webpack --config ./build/prod.config.js",		//生产时
        "dev": "webpack-dev-server --open --config ./build/dev.config.js"		//开发时
    }
}
~~~

***注意修改dist拼接路径：在base.config.js里面putput里的path项的 path.resolve(__dirname, '../dist')***

### 16 Vue CLI 俗称脚手架

如果npm 安装慢,可以用cnpm淘宝镜像

使用方法：

~~~ 
npm install -g cnpm --registry=http://registry.npm.taobao.org
~~~

之后就可以使用cnpm了

#### 16.1 安装

~~~ 
npm install -g @vue/cli		//全局安装脚手架3
~~~

拉取2.x版本

~~~ javascript
npm install -g @vue/cli-init
~~~

vue CLI2初始化项目：

~~~ javascript
vue init webpack my-project
~~~

#### 16.2 runtime+compiler和runtime-only的区别

runtime-only性能更高，代码量少

runtime-only里面没有了template，直接进行render（）

#### 16.2 Vue CLI3

创建项目：

~~~ javascript
vue create 项目名称
~~~

#### 16.3 路由

hash和history可以在改变url的情况下使页面不刷新

~~~ javascript
location.hash = '';
history.pushState();		//可以前进后退
history.replaceState();		//不可以前进后退
history.go(1);			//网页前进
~~~

##### 16.3.1 配置路由

##### 在src下面的router文件夹内的index.js里面配置路由信息，没有则单独创建

~~~ javascript
import Router form 'vue-router';		//导入路由
import Vue from 'vue';			//导入vue
Vue.use(Router);				//通过vue.use(插件)使用插件
cons router = new Router({		////创建Router对象
    routes: [
        					//配置路由和组件之间的映射关系
    ]
})
export default router;		//导出
~~~

之后再主要js文件导入挂载就可以了

~~~ javascript
import router form './router'
new Vue({
    el: '#app',
    router: router,
    ...
})
~~~

##### 16.3.3 使用路由步骤：

1 创建路由组件

就是创建.vue组件

2 配置路由映射：组件和路径关系

~~~ javascript
import Home from '../components/Home'
import About from '../components/About'

const router = new Router({
routes: [
   {
    path: '',					//这里使页面重定向，可以默认显示首页
    redirect: '/home'
  },
  {
    path: '/home',        //url
    component: Home       //组件
  },
  {
    path: '/about',     //url
    component: About    //组件
  }
],
    mode: 'history'			//转换为history模式
})
~~~

3 使用路由：通过\<router-link>和 \<touter-view>

~~~ javascript
<template>
  <div id="app">
    <router-link to="/home">首页</router-link>
    <router-link to="/about">关于</router-link>
    <router-view></router-view>			//代表显示的位置
  </div>
</template>
~~~

##### 16.3.4 router-link 属性 

- to：用于指定跳转的路径
- tag: 可以指定\<router-link>之后渲染成什么组件，比如可以把代码渲染成一个\<li>而不是\<a>
- replace（只写一个属性即可） 可以使页面没有跳转功能
- active-class:  每个活动的router-link标签会被添加active-link-active类,此属性可以改变类的名字(也可以在路由配置里面的linkActiveClass里面更改)

##### 16.3.5 通过代码方式跳转路由

因为自带$router属性

~~~ javascript
  methods: {
    homeClick() {
      // this.$router.push('/home')			
      this.$router.replace('/home')				
    },
    aboutClick() {
      // this.$router.push('/about')
      this.$router.replace('/about')
    }
  }
~~~

##### 16.3.6 动态跳转路由

1 可以在URL后面显示信息，比如用户名

步骤：

首先在路由路径后面加上：

~~~ javascript
...
{
    path: '/user/:userId',		//  :ueerId 可以随便起
    component: User 
}

~~~

然后在组件属性to后面加上要显示的内容即可：

~~~ javascript
<router-link to='/user/zhangsan'>用户</router-link>
~~~

要从URL获取用户名可以用$toute.params.步骤里面“：”后面随便起的名字 （$route 和$router不一样，$route为当前活动的路由)

##### 16.3.7 路由懒加载

1 方法1： 结合Vue的异步组件和Webpack的代码分析（早期写法）



2 AMD写法：

~~~ javascript
const About = resolve => require(['../components/About.vue'], resolve)
~~~

3 ES6中的写法：

~~~ javascript
const Home = () => import('../components/Home.vue')
~~~

例子： 

``` javascript
{
    path: '/home',        
    component: () => import('../components/Home')
  },
```

##### 16.3.8 路由嵌套

步骤：

1. 创建对应的子组件，并且在路由映射中配置对应的子路由

   在每个路由里面的children属性里面添加即可

~~~ javascript
routes: [
    ...
    {
        path: ''
        component: ''
        children: [				//子属性路由
          {
        	path: 'news'		//子路由不写
        	component: ''
          }
        ]
    }
]
~~~

2. 在组件内部使用\<router-view>标签

~~~ javascript
<template>
  <div>
    <div>我是首页</div>
    <p>我是首页内容，发sad法赛as大赛发</p>
    <router-link to="/home/news">新闻</router-link>		//注意这里的to属性里面写完整的路径
    <router-link to='/home/message'>信息</router-link>

    <router-view></router-view>
  </div>

</template>
~~~

##### 16.3.9 传递参数

传递参的方式：

**parans类型：**

- 配置路由格式： /router/:id
- 传递的方式： 在path后面跟上对应的值
- 传递后形成的路径： /routr/123/router/abc

**query的类型：**

- 配置路由格式： /router, 也就是普通配置
- 传递的方式： 对象中使用query的key作为传递方式
- 传递后形成的路径： /router?id=123,/router?id=abc

~~~ javascript
传参数：
<router-link :to="{path: '/profile',query: {name: 'jjk',age: 12}}">档案</router-link>
接参数：
$route.query
~~~

##### 16.3.10 全局导航守卫

在路由进行切换的时候做一些事情

首先在路由里面配置meta属性：

~~~ javascript
{
  path: '',
  component: '',
    meta: {				//	meta就是数据里面的数据
      title: '首页'
    },
}
~~~

然后使用beforeach方法：（前置守卫，在跳转之前调用）

~~~ javascript
router.beforeEach((to, form, next) =>{			//to，和from为路由对象
  document.title = to.matched[0].meta.title		//to可以理解为$route 如果是有嵌套的话matched[0]就是拿到第一个
  next()			//必须调用，调用该方法，才可以进入下一个钩子
})
~~~

**补充：**

1. 如果是后置钩子，也就是afterEach,不需要主动调用next()函数
2. 还有其他守卫，详询官网

##### 16.3.11 keep-alive

keep-alive是Vue内置的一个组件，可以使被包含的组件保留状态，或避免重新渲染

属性：

- include 字符串或正则表达式，自由匹配的组件会被缓存
- exclude 字符串或正则表达式，任何匹配的组件都不会被缓存

##### 16.3.12 给文件夹起别名

在webpackbase.config.js里面：

~~~ javascript
  resolve: {
    extensions: ['.js', '.vue', '.json'],
    alias: {
      '@': resolve('src'),			//这里的@就是起了别名，代表src文件夹
    }
  },
~~~

使用过程中用别名就可以了，但如果是属性里面的路径比如src就需要在使用别名时在别名的前面加上“~”

### 17 Promise

使用：

~~~ javascript
  new Promise((resolve, reject) => {	//resolve,reject为必写
    setTimeout(() => {		//这里写异步的函数名称
      resolve('')		//	请求成功调用then
      reject('')		//请求失败调用catch
    }, 1000)
  }).then(() => {
						//这里写函数内容
  }).catch(() => {
    			//失败时执行的函数内容
  })

另一种写法是在then()里面传入两个函数，一个成功的函数，一个失败的函数
~~~

#### 17.2 Promise 链式调用

~~~ javascript
Promise.all(new Promise(), new Promise()).then(results => {			//results是一个数组，存放的是各网络请求的结果
})

~~~

#### 18 Vuex

1 安装：

~~~ javascript
npm install vuex --save
~~~

2 创建对象：

~~~ javascript
const store = new Vuex.Store({
  state: {				//state为想要共享的数据
    counter: 1000
  },
  mutations: {					//修改数据需要通过mutations 修改,参数传入state
    increment(state) {
      state.counter++
    },
    decrement(state) {
      state.counter--
    }
  },
  actions: {

  },
  getters: {

  },
  modules: {

  }
})

export default store;
~~~

3 使用：

~~~ javascript
$store.state.counter			//在别的组件使用$store.state就可以使用共享里面数据
this.$store.commit('increment') //在别的组件里使用commit函数执行mutations里面的函数以修改数据，参数传入函数名字
~~~

4 安装tevtool扩展程序

##### 18.2 getters

类似计算属性

~~~ javascript
getters: {
    powerCounter(state) {
      return state.counter * state.counter
    }
  },
~~~

使用： 

~~~ javascript
$store.getters.powerCounter
~~~

如果getters需要传入参数：

~~~ javascript
getters: {
    ...
    acer(statw) {
		return function(age) {		//可以以返回函数的形式得到参数，这样在调用时就可以传入参数了
            return state.students.filter(s => s.age > age)
        }	
  }
}
~~~

##### 18.3 mutation

可以传递额外参数

##### 18.4 mutation响应规则

- 提前在store中初始化好的属性
- 当给store中的对象添加新属性时，使用以下方式：
  - 使用Vue.set(obj, 'new Prop', 134)添加， Vue.delete(obj, 'age')删除
  - 用新对象给就对象重新编辑

***官方简洁在mutation里面的函数名用常量表示，就是把函数名单独抽出来放在一个js文件里面定义成常量***

##### 18.5 Action

Action 类似于Mutation，用来代替mutation进行异步操作

步骤：

1 在action里面写异步函数

~~~ javascript
actions: {
    actionChange(context) {		
      setTimeout(() => {
        context.commit('addadd')		//这里不可以写具体的操作，要必须经过mutation才可以改数据，所以用contextcommit()调用mutation里面的函数
      }, 1000)
    }
  },
~~~

2 调用action里面的方法

~~~ javascript
addText() {
      // this.$store.commit('actionChange')
      this.$store.dispatch('actionChange')	//要用dispatch调用action里面的方法
    }
~~~

##### 18.5 modules

可以将store分割成多个模块,每个模块有自己的state,mutations,action,getters等

1 声明：

~~~ javascript
modules: {
    a: moduleA		//module单独定义了
  }
~~~

2 使用：

~~~ javascript
$store.state.a.name  //这里的a就是模块，后面直接属性名
~~~

**注意在action,getters的参数问题**

### 19 网络模块封装 axios

**1 安装：**

~~~ javascript
npm install axios --save
~~~

**2 使用：**

~~~ javascript
axios({
  url: 'http://123.207.32.32:8000/home/multidata',
  method: 'get'
}).then(res => console.log(res))
~~~

#### 19.2 并发请求

使用axios.all()方法

~~~ javascript
axios.all([axios(), axios()]).then(results => {})
~~~

使用axios.spread可将数组展开

#### 19.3 全局配置

可以进行抽取，也可以利用axios全局配置

~~~ javascript
axios.defaults.baseURL = '192.168.0.1'
axios.defaults.headers.post['Content-Type'] = ''
~~~

#### 19.4 axios实例

使用axios实例请求数据

``` javascript
acios.creat({})
```

##### 19.5 axios拦截器

请求拦截器：

~~~ javascript
instance.interceptors.request.use(config => {
    ...			//操作代码，比如：config中的一些信息不符合服务器的要求，比如每次发送网络请求是，都希望在界面中显示请求中图标，比如某些王丽请求（登录（token）,必须携带一些特殊的信息
	return config		//返回config
  }, err => {
    
  })
~~~

响应拦截器： 

~~~ javascript
instance.interceptors.response.use()
~~~

