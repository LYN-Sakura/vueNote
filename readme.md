### 增加写Vue体验的vscode插件
* vetur
* vue 2 snippets
* one dark pro
* prettier-code formattor		格式化

### npm
* yarn -g

### 设计思想
1. mvc
	* 后端架构思想
2. mvvc
	* 前端架构思想
		* m : `model`
			* 数据层 **Vue**中 数据层都放在data中
		* v : `view`视图
			* **Vue**中`view`即我们的HTML页面
		* vm : `view-model` 控制器 将数据和视图建立关系
			* `vm`即 **Vue** 的实例 就是 vm

![mvvm形象图](./images/mvvm形象图.jpg)


### vue基础语法参数
> 语法 ： new Vue({参数：value})
```
el 				//挂载，关联
data 			//模型数据（值是一个对象）
methods 	※	//存放函数（值是一个对象）；无缓存
computed 	※	//计算属性，存放函数（值是一个对象）;让模板变得更加简单；有缓存
watch			//侦听器;存放函数（值是一个对象）；函数名为要监听的吧变量名；函数第一个形参为输入的值
directives		//局部自定义指令
filters			//局部过滤器
{{ }} 			//插值表达式，将数据填充在页面，支持一些js计算
```
> ※ 注意事项
* `methods` 和 `computed` 的区别
	1. 使用的时候`computed`不需要加()
	2. 是否缓存：计算属性是基于它们的依赖进行缓存的；_通俗点说：数据（依赖）没有改变时，计算同样的结果没有必要计算两次_	

	
### 指令
>注意：指令的本质是自定义属性

|指令											|作用											|  有无参数							|
|-- |-- | -- |
|v-cloak										|解决编译闪动；不常用							|      无							|
|v-text											|同{{}}作用,不解析html标签						| 有								|
|v-html											|同{{}}作用,解析html标签，容易遭受xss攻击		|  有								|
|v-pre											|阻止解析后面的{{msg}}，不常用					|  无								|
|v-once											|不在监听此数据，提高性能，不常用				|无									|
|v-model	※									|数据双向绑定									|有									|
|v-on:事件 = "fun"	※					| 绑定事件；简写：`@事件 = "事件"`;fun可以带()	| 有								|
|v-bind:属性 = "value"							| 绑定属性；简写：`:属性= "value"`				| 有,参数可为数组/对象；**自己体会**|
|v-if="条件"		※						| 满足判断条件，显示所在标签					| 有								|
|v-else="条件"									| 满足判断条件，显示所在标签					| 无								|
|v-else-if="条件"								| 满足判断条件，显示所在标签					| 有								|
|v-show="条件"	※						| 控制元素样式是否显示；相当于更改display		| 有								|
|v-for="(value,index) in 数组" :key="value.id" 	※	| 遍历数组;一定要加:key=>提高效率				| 有								|
|v-for="(value,key,index) in 对象"				| 遍历对象						| 有								|

>  ※  注意事项	
* v-model : 限制在`<input>`、`<select>`、`<textarea>`、`components`（组件）中使用
	
	--------------------------------------------------
	>语法：v-model.表单修饰符
	
	|表单修饰符	|作用						|
	|--|--|
	|number		|转化为数值					|
	|trim		|去掉开始和结尾的空格		|
	|lazy		|将input事件切换为change事件|


* v-on:事件="fun" 
	1. 当fun不带()时，函数中的第一个形参传回当前事件对象
	2. 当fun带()时，函数中有一个 **固定的实参** `$event`代表当前事件对象；`$event.target`是dom对象
	--------------------------------------------------
	>语法：v-on:事件.事件修饰符	
	
	|事件修饰符	|作用			|
	|-- |-- |
	|stop		|阻止冒泡		|
	|prevent	|阻止默认行为	|
	
	>注意事项
	
	1. 修饰符可以串联
	2. 事件后面有修饰符的时候可以不加参数
	--------------------------------------------------
	>语法：：v-on:键盘事件.按键修饰符	
	
	|按键修饰符	|作用				|
	|-- |-- |
	|enter		|按下回车			|
	|delete		|按下delete删除键	|
	|其他请参考vue官网		|[vue按键修饰符点此跳转](https://cn.vuejs.org/v2/guide/events.html#%E6%8C%89%E9%94%AE%E4%BF%AE%E9%A5%B0%E7%AC%A6)	|
	
	```js
	//自定义键盘修饰符，名字自定义，但是对应的值要对应键盘码(e.keyCode)的值
	Vue.config.keyCodes.fl = 112
	//获取键盘码
	methods:{
		fun(e){
			console.log(e.keyCode)
		}
	}
	```
	```html
	<!-- 快捷写法 -->
	<input type="text" @keydown.35="fun" v-model="age">
	```
	
* `v-if` 和 `v-show`的区别
	1. `v-if`控制元素是否渲染到页面
	2. `v-show`控制原始是否显示（已经渲染到页面）

* `v-for`中key的作用
	
	1. key属性可以用来提升v-for渲染的效率！，vue不会去改变原有的元素和数据，而是创建新的元素然后把新的数据渲染进去
###  什么是双向数据绑定？
>实现双向绑定的指令是`v-model`
```
当数据发生变化的时候，视图也就发生变化
当视图发生变化的时候，数据也会跟着同步变化
```
```html
<!-- 双向绑定原理代码 -->
<input v-bind:value="msg" @input="msg=$event.target.value" />
```

### 自定义指令
[官网CV它不香吗？](https://cn.vuejs.org/v2/guide/custom-directive.html#ad)

```js
//cv =>复制粘贴
// 注册一个全局自定义指令 `v-focus`
Vue.directive('focus', {
  // 当被绑定的元素插入到 DOM 中时……
  inserted: function (el) {
    // 聚焦元素
    el.focus()
  }
})
// 注册一个局部自定义指令 `v-focus`
directives: {
  focus: {
    // 指令的定义
    inserted: function (el) {
      el.focus()
    }
  }
}
```


### 过滤器
[官网CV它不香吗？](https://cn.vuejs.org/v2/guide/filters.html#ad)

```html
<!-- cv =>复制粘贴 -->
<!-- 在双花括号中; | : “管道”符号 -->
{{ message | capitalize }}

<!-- 在 `v-bind` 中 -->
<div v-bind:id="rawId | formatId"></div>
```

```js
// 注册一个全局过滤器 
Vue.filter('capitalize', function (value) {
	if (!value) return ''
	value = value.toString()
	return value.charAt(0).toUpperCase() + value.slice(1)
})

// 注册一个局部过滤器 
filters: {
	capitalize: function (value) {
		if (!value) return ''
		value = value.toString()
		return value.charAt(0).toUpperCase() + value.slice(1)
  }
}
```

### 补充知识
* 修改响应式数据
	```js
		//参数详解：list:vue实例中的数组/对象数据，index：下标/属性，value：将数据修改成value
		Vue.set(list,index,value)
		//参数详解：vm:储存vue实例的变量，其余参数同上，效果同上，只是语法不同
		vm.$set(list,index,value)
	```

--------------------------------------------------

### vue进阶=>[组件](https://cn.vuejs.org/v2/guide/components.html#ad)
>以下笔记不在写的非常详细，学会查看官方文档；下方将带一脚重要知识点

### 父组件向子组件传值
* 属性绑定
	1. 在`自定义`组件标签上绑定`自定义`属性
	2. 给此属性赋予值(静态/动态)
	3. 这个值通过`props`捕捉到
	4. `props`属性的参数可以是数组，捕获多个`自定义`属性
	5. 将捕获到的属性传入`template`中
	6. 注意`自定义`属性不建议`驼峰命名法`
	7. 注意`自定义`属性使用中间用`-`隔开的命名时可以用 `驼峰命名法`捕获

### 子组件向父组件传值
* 事件绑定
	
	```
	//参数详解：
	//固定参数： $event=>接受参子组件参数
				$emit()=>提供事件名和参数
	//自定义参数：事件名=>自定义，两个事件名保持一致
				 fun=>自定义函数，位于父组件中
	//注意：$emit()位于子组件模板中,另一个位于父组件模板中
	@事件名 = "fun($event)"
	@click = '$emit("事件名",value)'
	```
		
### 非父子组件间传值

	1. 单独的事件中心管理组件间的通信
	2. 监听事件与销毁事件
	3. 触发时间
	4. 被`vuex`替代，以上仅作了解

### 插槽
* 固定标签/具名插槽
```html
<!--页面中  -->

<!-- slot 与 name 一一对应 -->
<abc>
	<div slot = "header"></div>
	<div></div>
	<div slot = "footer"></div>
</abc>

<!-- 放在子组件template中 -->
<slot name="header">默认内容</slot>
<slot >默认内容</slot>
<slot name="footer">默认内容</slot>

<!-- template 临时包裹 页面中不会显示-->
	<template name = "main">
	
	</template>
```
* 作用域插槽
待定

### restful形式的URL
	1. get		查询
	2. post		添加
	3. put		修改
	4. delete	删除

### 接口调用-fetch

```js
fetch("url",{
	//设置一些选项
	methed:'get',
	//下面为post/put传参需要添加的选项
	body:"name=44&pwd=2222",
	headers:{
		"Content-Type":"application/x-www-form-urlencoded"
	}
	//另一种post传递的参数为json格式
	//需要用JSON的转字符串方法	
	body:JSON.stringify({
		name:55,
		age:55
	}),
	headers:{
		"Content-Type":"application/json"
	}
	
}).then(function(data){
	//text属于fetch一部分，返回promise对象
	return data.text()
	//json数据获取推荐，使用text获取的是字符串，需要转换json.prase()
	return data.json()
}).then(function(data){
	//这里才是最终数据
	console.log(data)
})
```

### 接口调用-axios	！重点


```js
//get 请求
axios.get("url"，{
	params:{
		//get的参数
	}
}).then(ret=>{
	//data属性名称是固定的,用于获取后台响应的数据
	console.log(ret.data)
})
//另一种写法
async function fn(){
	let {data}=await axios.get("http://localhost:3000/adata",{
		//推荐掌握的传递参数方式
		params:{
			//get的参数
		}
	})
	console.log(data)
}

//post请求
async function fn() {
	let { data } = await axios.post('http://localhost:3000/axios', {
		uname:22,
		pwd:2222
	});
	console.log(data);
}

// 全局配置


axios.defaults.timeout = 3000 //超时时间
axios.defaults.baseURL = 'http://localhost:3000/'	//默认地址
axios.defaults.headers['自定义名称'] = "hello"	//请求头			

```


### 前端路由
* 路由
	1. 后端路由
		`概念`：根据不同的用户`URL请求`，返回不同的内容
		`本质`：`URL请求地址`与`服务器资源之间`的对应关系
	2. 前端路由
		>SPA（Single Page Application）
		* 后端渲染（存在性能问题）
		* Ajax前端渲染（前端渲染提高性能，但是不支持浏览器前进后退操作）
		* SPA 单页面应用程序；整个网站只有一个页面，内容的变化通过Ajax局部更新实现，同时支持浏览器的前进和后退操作
		* SPA实现原理之一：基于URL地址的hash(hash的变化会导致浏览器记录访问历史的变化，但是hash的变化不会触发新的URL请求)
		* 在实现SPA过程中，最核心的技术点就是前端路由
	
	
>了解
	
	* 历史模式：	history.pushStatus

* 具体实现代码如下
```js
<div id="app">
	//路由链接
	<router-link to="shan">看这山</router-link>
	<router-link to="shui">看这水</router-link>
	//显示的区域
	<router-view></router-view>
</div>
<script type="text/javascript">
	//储存模板的常量
	const shan = {
		template: `<div>这是山</div>`
	};
	const shui = {
		template: `<div>这是水</div>`
	};
	//路由实例
	const router = new VueRouter({
		routes:[{
			//path:页面中写的地址 ，也就是 to="URL" 中的URL
			path:"/shan",
			//上方定义好的常量模板
			component:shan
		},
		{
			path:"/shui",
			component:shui
		}]
	})
	
	
	const vm = new Vue({
		el: '#app',
		//属性和参数相同，可以简写；启动路由
		router
	});
</script>
```