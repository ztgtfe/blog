---
layout: post
title:  "自定义JQuery 插件"
date:   2016-03-14 15:48:00 +0800
categories: 工具
---

# JQuery 插件写法，俗称"造轮子"

## JQuery的架构
JQuery 封装了DOM操作，并且具有很好的浏览器兼容性。
另外，JQuery使用了匿名函数自执行，拥有自己的命名空间，不会污染全局变量。
==匿名函数自执行：`;(function(){})()` ，`;`是为了隔断前面的代码。==  
下面是[jquery-2.0.3.js](http://xiaoxudoo.cn/images/jquery-2.0.3.js)的源码架构：
```js
(function(){
	
	(21 , 94) 定义了一些变量和函数 jQuery = function(){};
	
	(96 , 283) 给JQ对象，添加一些方法和属性
	
	(285 , 347) extend : JQ的继承方法
	
	(349 , 817) jQuery.extend() : 扩展一些工具方法
	
	(877 , 2856)  Sizzle : 复杂选择器的实现    //比较难的部分
	
	(2880 , 3042) Callbacks : 回调对象 : 对函数的统一管理
	
	(3043 , 3183) Deferred : 延迟对象 : 对异步的统一管理
	
	(3184 , 3295) support : 功能检测
	
	(3308 , 3652) data() : 数据缓存
	
	(3653 , 3797) queue() : 队列方法 : 执行顺序的管理 
	
	(3803 , 4299) attr() prop() val() addClass()等 : 对元素属性的操作
	
	(4300 , 5128) on() trigger() : 事件操作的相关方法
	
	(5140 , 6057) DOM操作 : 添加 删除 获取 包装 DOM筛选
	
	(6058 , 6620) css() : 样式的操作
	
	(6621 , 7854) 提交的数据和ajax() : ajax() load() getJSON()
	
	(7855 , 8584) animate() : 运动的方法
	
	(8585 , 8792) offset() : 位置和尺寸的方法
	
	(8804 , 8821) JQ支持模块化的模式
	
	(8826)  window.jQuery = window.$ = jQuery;
	
})();
```

注意第96行: `jQuery.fn = jQuery.prototype = {`

## 如何实现一个JQuery插件
**JavaScript的原型继承：**

* 自己的理解： JS通过原型继承使得对象实例带有**祖先**的方法、属性。
* 原型继承区别于类继承，在面向对象中，并不存在一个封装好的类（Class），而是通过构造函数+原型链来完成。 ==ps：es6中新增了class==
* 这一部分内容欢迎大家参考：[JavaScript设计模式与开发实践](http://item.jd.com/11686375.html)第一部分的内容，对理解原型继承很有帮助。

回到上面说的JQuery源码第96行，jQuery.fn指向了jQuery对象的原型，
因此需要扩展jQuery的方法只需要在jQuery.fn上定义，所以制作插件的一般流程是：
```js
(function($){
	$.fn.method = function(settings){
		settings=$.extend({},$.method.defaults,settings);
	};
	$.method = {defaults:{}};
})(jQuery)
```
另外注意到最后一句`window.jQuery = window.$ = jQuery;` 他把jQuery变成了全局变量，在外部也能使用
   	
* 结论：
  另外举两个插件的例子：
  @xiaohuiui [分页插件AMD版](http://yinxiazi.com/static/js/pc/paging.js);
  @xiaoxudong [银匣子底部合作机构移动插件修改版](http://yinxiazi.com/static/js/jquery.cxscroll.js);
  插件的目的就是扩展了JQuery对象能使用的方法，来完成一些内部我们不需要知道的操作(就是'轮子'的意味)。

## 参考：
> 1. [妙味课堂--JQuery源码分析](http://jquery.miaov.com/)
> 2. [JavaScript设计模式与开发实践](http://item.jd.com/11686375.html)
> 3. [jQuery插件库](http://jq22.com/)

`ps: 这里仅是个引子，大家在实际开发中如果碰到什么jquery插件问题，可以@这篇内容继续讨论。
例如：
@xiaoxudong 我有一个问题blabla`
