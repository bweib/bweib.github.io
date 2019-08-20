<!--
 * @Description: In User Settings Edit
 * @Author: your name
 * @Date: 2018-12-22 21:28:35
 * @LastEditTime: 2019-08-20 23:41:35
 * @LastEditors: Please set LastEditors
 -->
---
layout: post
title:  "实现文本域输入字数的限制"
date:   2018-01-02 14:08:41
category: "Other"
categories: jekyll blog
---
#### 我们在QQ空间发表说说发微博的时候，会有140字的字数限制。今天我们也来把这个简单的效果做出来，刚好是项目中遇到的小问题。在此记录下来。

#### 上代码:
```js
$("textarea").on("input propertychange", function() { 
var $this = $(this), 
_val = $this.val()； 
//限制200字 
if (_val.length > 200) { 
$this.val(_val.substring(0, 200)); 
} 
count = 200 - $this.val().length; 
$("#text-count").text(count); 
}); 
```
the end.

