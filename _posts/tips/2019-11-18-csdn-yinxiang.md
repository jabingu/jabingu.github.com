---

layout: post
title:  "CSDN印象笔记剪藏正文内容"
date:   2019-11-18 07:19:54
categories: tips
tags: tips
thumbnail: "assets/img/post/tips.jpg"
feature-img: "assets/img/post/tips.jpg"
excerpt: CSDN印象笔记剪藏正文内容
---

* content
{:toc}
>  问题：查看CSDN文章的时候，发现会有好的文章，想要保存在印象笔记中，使用剪藏功能时候发现会剪藏所有的内容，而没有办法保存正文 



## 思路：

1. 百度快照
2. 隐藏广告模式
3. 选中内容模式
4. 网页处理只显示正文



## 百度快照

 e，显示的什么玩样？ 

## 隐藏广告模式

 存在问题：**没有保存格式**；可阅读性降低 

## 选中内容模式

1. 使用鼠标选中标题和正文的内容
2. 再去点击印象笔记的剪藏图标

结果：成功，剪藏后的内容整体可以，**但是每一行的文字会很长**。

## 网页处理只显示正文

>  参考的是打印CSDN正文的方法。先把网页处理只显示正文，再进行剪藏就可以了。 

1. **F12**进行开发者模式
2. 进入`Console`,输入代码
3. 最后进行剪藏就可以了。

**代码如下：**

```js
(function(){
$("#side").remove();
$("#comment_title, #comment_list, #comment_bar, #comment_form, .announce, #ad_cen, #ad_bot").remove();
$(".nav_top_2011, #header, #navigator").remove();
$(".p4course_target, .comment-box, .recommend-box, #csdn-toolbar, #tool-box").remove();
$("aside").remove();
$(".tool-box").remove();
$("main").css('display','content'); 
$("main").css('float','left'); 
//window.print();

$("tool-box").remove();
})();
```

> 这里代码和原有的不同的地方是：**把“打印”这个函数注释掉**。
>





## 参考文献

[打印CSDN网页内容](https://blog.csdn.net/u010954948/article/details/82843105)