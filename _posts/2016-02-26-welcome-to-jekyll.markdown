---
layout: post
title:  "我该怎样写一篇JekyII博客"
date:   2016-03-10 00:48:47 +0800
categories: 工具
---
我们在Github上的博客已经搭建了两周了，但是还没有一篇博客在上面，可能是大家对JekyII这种静态博客、Git和Github不熟悉的原因吧。我就在这写一篇发博客的流程，再附上一些Git的教程，算抛砖引玉之言。

1. 首先，你得有自己的github的账号，登录。然后来到我们博客的页面[https://github.com/ztgtfe/ztgtfe.github.io](https://github.com/ztgtfe/ztgtfe.github.io)
2. 在页面的右上角点击fork，将博客的仓库fork到自己的github上![先fork到个人仓库里](http://7mnlto.com1.z0.glb.clouddn.com/2016-03-10%2001-09-35.png)
3. 在自己的github里拷贝git链接![拷贝git链接](http://7mnlto.com1.z0.glb.clouddn.com/2016-03-10%2001-13-52.png)
4. 在本地的命令行工具里git clone，然后打开你本地的项目地址，

	```
	git clone https://github.com/LeonWhite/ztgtfe.github.io.git
	```
	然后你可以看到这样的目录结构
	```
|____.git
|____.gitignore
|_____config.yml
|_____includes		//存放页面子模板
|_____layouts		//存放页面模板
|_____posts			//存放blog内容
|_____sass			//存放基本样式
|____about.md		//关于我们的模板
|____css				//存放页面样式
|____feed.xml		//存放反馈的数据
|____index.html	//主页
```
5. 要新建一篇博客很简单，只需要在_posts文件夹下新建一个markdown文件就行，命名规范是“日期-博客名.markdown”，比如
`2016-03-03-test.markdown`
*需要强调的是文件名里不能有空格*
6. 在博客的内容中，需要注意的是在开头部分需要添加[YAML](http://yaml.org/)头信息，像这样：

	```
	---
	layout: post
	title:  "我该怎样写一篇JekyII博客"
	date:   2016-03-10 00:48:47 +0800
	categories: 工具
	---
	```
==头信息非常重要，文章在网站显示的最终的标题其实定义在这里，还有分类、时间、模板等等。具体可以看看YAML的文档==
7. 具体博客的内容用markdown来编写，可以参考[Markdown语法和MWeb](http://ztgtfe.github.io/%E5%B7%A5%E5%85%B7/2016/02/26/Markdown-syntax-guide-and-writing-on-MWeb.html)
8. 博客写完，在git上操作：
	```
	git add .
	git commit -m"POST Blog 2016-03-10-test.markdown"
	git push https://github.com/LeonWhite/ztgtfe.github.io.git master
	```




