title: Hexo博客集成友言评论系统教程
author: 无知の人
tags:
  - Hexo
categories:
  - 研究
date: 2017-07-28 16:58:00
origin: true
---
前言
------------
之前博客评论使用的是 网易云跟帖，结果最近网易云跟帖官方发布公告，将在8月1日停止提供评论功能，导致博客内的评论功能在8月1日后就失效了，而Hexo博客的Yilia主题中只提供了畅言、网易云跟帖、多说和Disqus，其中畅言要求网站必须备案，Disqus是国外的很不稳定，网易云跟帖和多说已不再提供服务了，所以有必要尝试添加其他社会评论系统了！

在网上简单的找了下，发现“友言”的评论系统还不错，经过博主不懈努力，现已成功在Hexo博客中集成友言评论系统，如果有朋友也想在自己的Hexo博客中加入友言评论系统，那么请继续看下面的教程吧！

PS. 本教程仅在Hexo博客的Yilia主题中测试可用。友言的注册相关内容不再本文讨论范围之内，其实注册很简单也没必要写教程的。

<!-- more -->

教程
------------
首先打开目录

    \hexo\themes\yilia\layout\_partial\post

在目录下创建文件

    uyan.ejs

然后用记事本打开此文件，文件内容可复制粘贴如下代码

```
<!-- UY BEGIN -->
<div id="uyan_frame" class="article-entry article article-type-post" style="padding-top:50px;"></div>
<script type="text/javascript" src="http://v2.uyan.cc/code/uyan.js?uid=<%=theme.uyan%>"></script>
<!-- UY END -->
```

此文件关闭。然后记事本打开下面目录中的文件

    \hexo\themes\yilia\layout\\_partial\article.ejs
注意：是article.ejs，不是archive.ejs，两文件比较相像

通过Ctrl+F查找

    <% if (!index && post.comments){ %>

在此代码下方复制粘贴如下代码

```
  <% if (theme.uyan){ %>
  <%- partial('post/uyan', {
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
uyan: "你的友言ID"
```

注意：
1、“你的友言ID”为友言官方管理后台中提供的ID，用英文状态的双引号括起来
2、“uyan:”处冒号后面必须要有一个空格，这是Hexo博客的配置要求

至此友言的第三方评论系统就集成到你的Hexo博客中了。