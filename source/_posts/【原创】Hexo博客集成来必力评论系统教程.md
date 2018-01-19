title: 【原创】Hexo博客集成来必力评论系统教程
author: 无知の人
tags:
  - Hexo
categories:
  - 研究
date: 2018-01-19 11:52:17
---
前言
------------
之前用过网易云跟帖和友言评论系统，前者已经关闭，后者不清楚是官方的问题还是我个人网络的事，总是出现无法加载的现象，由于总总原因畅言和国外知名的Disqus都不能使用，所以之恩那个接受有言的不完美了。

不过最近在其他博友那里了解到还有一个评论系统，他的名字叫“来必力”，注册的时候会出现韩文，推断可能是来自韩国的社会评论系统，不过他是支持中文的，加载速度很快，而且功能也比较丰富，所以我的博客中就改用它了。

那么长话短说，下面开始。

<!-- more -->

教程
------------
首先打开目录

    \hexo\themes\yilia\layout\_partial\post

在目录下创建文件

    livere.ejs

然后用记事本打开此文件，文件内容可复制粘贴如下代码

```
<!-- 来必力City版安装代码 -->
<div id="lv-container" data-id="city" data-uid="<%=theme.livere%>" style="margin:30px;margin-top:20px;padding-left:6.5%;padding-right:6.5%;background-color:#ffffff;">
<script type="text/javascript">
   (function(d, s) {
       var j, e = d.getElementsByTagName(s)[0];

       if (typeof LivereTower === 'function') { return; }

       j = d.createElement(s);
       j.src = 'https://cdn-city.livere.com/js/embed.dist.js';
       j.async = true;

       e.parentNode.insertBefore(j, e);
   })(document, 'script');
</script>
<noscript>为正常使用来必力评论功能请激活JavaScript</noscript>
</div>
<!-- City版安装代码已完成 -->
```

此文件关闭。然后记事本打开下面目录中的文件

    \hexo\themes\yilia\layout\\_partial\article.ejs
    
注意：是article.ejs，不是archive.ejs，两文件比较相像

通过Ctrl+F查找

    <% if (!index && post.comments){ %>

在此代码下方复制粘贴如下代码

```
  <% if (theme.livere){ %>
  <%- partial('post/livere', {
      key: post.slug,
      title: post.title,
      url: config.url+url_for(post.path)
    }) %>
  <% } %>
```

粘贴后此文件可关闭。再找到下面目录中的文件用记事本打开

    \hexo\themes\yilia\\_config.yml

在空白处另起一行插入下面代码

```
livere: "填写注册来必力后给你的一串编码"
```

注意：“livere:”处冒号后面必须要有一个空格，这是Hexo博客的配置要求

至此来必力的第三方评论系统就集成到你的Hexo博客中了。