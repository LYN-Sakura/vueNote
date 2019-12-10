>目录
[toc]
### vscode插件
* vetur
* vue 2 snippets
* one dark pro

### vue基础语法
```
el //挂载，关联
data //模型数据（值是一个对象）
{{ }} //插值表达式，将数据填充在页面，支持一些js计算
```

### 指令
>注意这些指令都是标签中的属性

|指令	|											|  有无参数	|
|-- |-- | -- |
|v-cloak|解决编译闪动；不常用						|      无	|
|v-text	|同{{}}作用,不解析html标签					| 有		|
|v-html	|同{{}}作用,解析html标签，容易遭受xss攻击	|  有		|
|v-pre	|阻止解析后面的{{msg}}，不常用				|  无		|
|v-once	|不在监听此数据，提高性能，不常用			|无参数		|
|v-model|数据双向绑定								|有参数		|

* v-model 限制在`<input>`、`<select>`、`<textarea>`、`components`（组件）中使用

###  什么是双向数据绑定？
>实现双向绑定的指令是`v-model`
```
当数据发生变化的时候，视图也就发生变化
当视图发生变化的时候，数据也会跟着同步变化
```

### 设计思想
1. mvc
	* 后端架构思想
2. mvvc
	* 前端架构思想
		* m : model
			* 数据层 Vue中 数据层都放在data中
		* v : view视图
			* Vue中view即我们的HTML页面
		* vm : view-model 控制器 将数据和视图建立关系
			* vm即 Vue 的实例 就是 vm
![mvvm形象图](./images/mvvm形象图.jpg)