---
layout: post
title:  "tap点透bug"
date:   2016-03-10 12:20:00 +0800
categories: 移动开发
---

# Zepto.js 开发中的坑

## 移动开发框架
jquery对DOM操作的封装，在PC端运用广泛，*Zepto.js*仿照Jquery开发了一套相同的API适用于移动端。[Zepto 中文站](http://www.zeptojs.cn)
### 移动开发中click事件会出现**300ms**的延迟:

> 这要追溯至 2007 年初。苹果公司在发布首款 iPhone 前夕，遇到一个问题：当时的网站都是为大屏幕设备所设计的。于是苹果的工程师们做了一些约定，应对 iPhone 这种小屏幕浏览桌面端站点的问题。 
> 
> 这当中最出名的，当属双击缩放(double tap to zoom)，这也是会有上述 300 毫秒延迟的主要原因。双击缩放，顾名思义，即用手指在屏幕上快速点击两次，iOS 自带的 Safari 浏览器会将网页缩放至原始比例。 
> 
> 那么这和 300 毫秒延迟有什么联系呢？ 
> 
> 假定这么一个场景。用户在 iOS Safari 里边点击了一个链接。由于用户可以进行双击缩放或者双击滚动的操作，当用户一次点击屏幕之后，浏览器并不能立刻判断用户是确实要打开这个链接，还是想要进行双击操作。因此，iOS Safari 就等待 300 毫秒，以判断用户是否再次点击了屏幕。 
> 
> 鉴于iPhone的成功，其他移动浏览器都复制了 iPhone Safari 浏览器的多数约定，包括双击缩放，几乎现在所有的移动端浏览器都有这个功能。之前人们刚刚接触移动端的页面，在欣喜的时候往往不会care这个300ms的延时问题，可是如今touch端界面如雨后春笋，用户对体验的要求也更高，这300ms带来的卡顿慢慢变得让人难以接受。

因此zepto.js使用tap事件代替click解决这个问题，zepto整合了移动端的原生事件touch(start/move/end)开发了Touch模块，封装了移动端的常用事件，如点击（tap），长按（longTap），单击（singleTap）,双击（doubleTap）,滑屏（swipe）等。
详细的API在这里: [Zepto touch API](http://www.zeptojs.cn/#touch)

## 点透bug
*点透bug是一个Zepto tap事件的经典bug：

![示例图片](http://xiaoxudoo.cn/images/tap-bug.jpg)
==点击红色区域会触发蓝色区域的点击事件，俗称点透==

*点透bug的原因是：
1. tap事件实际上是在冒泡到body上时才触发
2. click事件的延迟触发

*目前的解决方案不一：
1. 简单粗暴的就是换回成click事件
2. fastclick库 + (Zepto.js - touch模块)
3. 自己写代码避免， 具体实现可能不同，如touchend + e.preventDefault
   	
*结论：
==在使用zepto框架的tap相关方法时，一定要注意，如果绑定tap方法的dom元素在tap方法触发后会隐藏、css3 transfer移走、requestAnimationFrame移走等，而“隐藏、移走”后，它底下同一位置正好有一个dom元素绑定了click的事件、或者有浏览器认为可以被点击有交互反应的dom元素（举例：如input type=text被点击有交互反应是获得焦点并弹起虚拟键盘），则会出现“点透”现象。在这种情况下，我们应当采用上述方法来避免“点透”。==
参考：
> 1. [悠悠工厂--前端](http://youyogmail-001-site1.site4future.com/archives/zepto-tap-click-through-research.html)
> 2. [移动端开发框架Zepto入门](http://www.imooc.com/learn/229)

`ps: 这里仅是个引子，大家在实际开发中如果碰到什么zepto tap问题，可以继续讨论`









