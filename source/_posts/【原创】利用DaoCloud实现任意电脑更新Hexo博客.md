title: 【原创】利用DaoCloud实现任意电脑更新Hexo博客
author: 无知の人
tags:
  - DaoCloud
  - Hexo
categories:
  - 研究
date: 2018-01-16 17:19:47
---
##前言
Hexo也用了有一段时间了，有点太多了就不再一一列出了，不过弊端也是有的，例如更新博客必须要在本地的电脑上搭设Hexo本地程序，实在是不方便维护，最近研究了一种可以脱离本地程序，完全线上更新Hexo博客的方式，这样就可以在任意一台电脑上进行维护了，那么废话不多说，下面开始讲解方法。

##注册Github和搭建本地Hexo环境
关于注册Github我之前发布过文章，【[点击这里](http://baipai.tk/2017/05/11/%E3%80%90%E5%8E%9F%E5%88%9B%E3%80%91%E5%B0%8F%E7%99%BD%E6%95%99%E4%BD%A0%E6%89%8B%E5%8A%A8%E6%90%AD%E5%BB%BAHexo%E5%8D%9A%E5%AE%A2%EF%BC%88Win%E7%89%88%EF%BC%89/)】可以查看注册和搭建Hexo方法。

<!-- more -->

##配置GitHub
1、在本地Hexo源码的根目录创建Dockerfile文件，文件内容如下：

```
FROM node:slim
MAINTAINER GitHub用户名 <GitHub注册邮箱>
# instal basic tool 
RUN apt-get update && apt-get install -y git ssh-client ca-certificates --no-install-recommends && rm -r /var/lib/apt/lists/*
# set time zone
RUN echo "Asia/Shanghai" > /etc/timezone && dpkg-reconfigure -f noninteractive tzdata
RUN npm install
# install hexo
RUN npm install hexo-cli -g
# install hexo server
RUN npm install hexo-server
# set base dir
#RUN mkdir /hexo
# set home dir
#WORKDIR /hexo
EXPOSE 4000
#CMD ["/bin/bash"]
```

2、创建新的Github仓库，将原先本地的Hexo博客源代码，发布到这个新建的仓库

##注册DaoCloud
如果要实现上面的方法就要使用到DaoCloud的功能。

1、登录【[点击这里](https://www.daocloud.io/)】注册DaoCloud账号

2、点击“创建新项目”项目，依次填写

* 项目名称：如“Test”
* 设置代码源：选择前面新创建的GitHub仓库
* 发布应用镜像：默认选择“镜像仓库”

3、进入创建的项目 > 流程定义 > 点击右侧“通过yaml快速编辑”，在里面编辑如下内容

```
version: 2.0
test: 
    image: 【此处填写镜像地址】:latest  #填写镜像地址
    install: 
        - npm install
    before_script: 
        # 配置git全局的用户名和邮件地址
        - git config --global user.name "【Github用户名】"
        - git config --global user.email "【Github的注册邮箱】"
    script: 
        - hexo clean
        - hexo g
        - hexo d
build: 
   image: 
       dockerfile_path: Dockerfile
       build_dir: /
       cache: true
```

注意：修改“【】”中的内容，代码中不包含“【】”。

##完成
至此配置完成，只要新建仓库中的内容发生改变，DaoCloud舅会自动更新Hexo博客的内容，你可以通过GitHub Disktop软件更新仓库中文件内容，也可以直接在网上手动创建、编辑MD文件来更新Hexo。