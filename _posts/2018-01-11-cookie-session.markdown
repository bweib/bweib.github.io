---
layout: post
title:  "浅谈cookie/session与的生命周期"
date:   2018-01-11 14:58:41
category: "Other"
categories: jekyll blog
---

<p>最近在学习浏览器的cookie和session.查阅了网上的资料还有加上我个人的理解，整理了一些关于cookie/session 的知识。请听我娓娓道来。</p>    
<p>什么是cookie?</p>
cookie是浏览器存储信息的方案。
<p>它可以用来存储一些临时信息。如登陆名，密码的缓存cookie是分域名进行存储的，每个域名下面能够存储的cookie大小为4k。cookie中存储的信息，可以被所有的当前域名下的页面共享！But，cookie是有目录限制的，根目录设置的cookie可以在所有的目录下进行访问然而子目录中设置的cookie父目录中并不能访问。这种cookie被称为会话cookie。其一般不保存在硬盘上.而是保存在内存中。</p>
<p>cookie的应用：
     我们一般不会在cookie中存储大量的数据，原因如下：
     1. 容量太小，一般浏览器中的cookie容量只有4K，转成中文也就是几千个汉字。
     2. 由于每次请求都会携带cookie信息，所以会影响传输效率，访问速度！</p>
<p>cookie的生命周期</p>
<p>如果cookie不设定时间的话就表视它的生命周期为浏览器会话的期间,只要关闭浏览器,cookie就消失了。

如果设置了cokie的过期时间.那么浏览器会把cookie保存到硬盘中,再次打IE时会依然有效.直到超过设置的有效期

$.cookie(key, value, {path:"/", expire: new Date("2017-01-01")})  设置过期时间。

注:存储在硬盘中的cookie可以在不同IE间共享.</p>
<p>什么是session？</p>
session是在服务端存储信息的方案。
当客户端发起一个HTTP请求时服务端会创建一个session.并分配一个sessionID作为服务端对客户端的识别。当服务器处理完后,会将sessionID同reponse 一起传回客户端,并将其存到cookie中，Session存储位置是在服务器端。一般为了防止在服务器的内存中（为了高速存取），Sessinon在用户访问第一次访问服务器时创建，需要注意只有访问JSP、Servlet等程序时才会创建Session，只访问HTML、IMAGE等静态资源并不会创建Session，可调用request.getSession(true)强制生成Session。

当客户端再发送请求的时候.会将sessionID连同request一起发送给服务端，服务端再根据传过来的sessionID将这次request与保存在服务端的session对象联系起来.此时的session对象已不是NEW STATE状态。

Session的生命周期

<p>1.服务器会把长时间没有活动的Session从服务器内存中清除，此时Session便失效。Tomcat中Session的默认失效时间为20分钟。

2.调用Session的invalidate方法。

注:当禁用cookie时也是不能使用session的.

 （根据网络资料整理）</p>