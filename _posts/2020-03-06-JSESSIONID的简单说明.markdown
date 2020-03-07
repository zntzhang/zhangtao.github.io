---
layout:  post
title:   JSESSIONID的简单说明
date:   2020-03-06 15:52
author:  "唐传林"
header-img: "img/post-bg-2015.jpg"
catalog:   false
tags:

---
**1）第一次访问服务器的时候，会在响应头里面看到Set-Cookie信息（只有在首次访问服务器的时候才会在响应头中出现该信息）**  
![在这里插入图片描述](http://img-blog.csdnimg.cn/20181222211057258.jpg)

上面的图 JSESSIONID=ghco9xdnaco31gmafukxchph;Path=/acr，

浏览器会根据响应头的set-cookie信息设置浏览器的cookie并保存之

注意此cookie由于没有设置cookie有效日期，所以在关闭浏览器的情况下会丢失掉这个cookie。

**2）当再次请求的时候（非首次请求），浏览器会在请求头里将cookie发送给服务器(每次请求都是这样)**  
![在这里插入图片描述](http://img-blog.csdnimg.cn/20181222211150839.jpg)

（JSESSIONID=ghco9xdnaco31gmafukxchph）

不难发现这个的jsessionid和上面的jsessionid是一样的

**3）为什么除了首次请求之外每次请求都会发送这个cookie呢（在这里确切地说是发送这个jsessionid）？**  
事实上当用户访问服务器的时候会为每一个用户开启一个session，浏览器是怎么判断这个session到底是属于哪个用户呢？  
jsessionid的作用就体现出来了：jsessionid就是用来判断当前用户对应于哪个session。  
（如果客户端请求的cookie中包含JSESSIONID，服务端调用request.getSession()时就会根据JSESSIONID进行查找对象，如果能查到就返回，否则就跟没传递JSESSIONID一样；）  
换句话说服务器识别session的方法是通过jsessionid来告诉服务器该客户端的session在内存的什么地方。  
事实上jsessionid ==request.getSession().getId()

**4)总结，jsessionid的工作流程可以简单用下面的图表示：**  
![在这里插入图片描述](http://img-blog.csdnimg.cn/20181222211223883.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzM3MjIxOTkx,size_16,color_FFFFFF,t_70)

