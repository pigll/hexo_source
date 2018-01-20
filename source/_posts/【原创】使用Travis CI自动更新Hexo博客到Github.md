title: 【原创】使用Travis CI自动更新Hexo博客到Github
author: 无知の人
tags:
  - Hexo
categories:
  - 研究
date: 2018-01-16 17:19:47
---
##### 前言 #####
Hexo也用了有一段时间了，有点太多了就不再一一列出了，不过弊端也是有的，例如更新博客必须要在本地的电脑上搭设Hexo本地程序，实在是不方便维护，最近研究了一种可以脱离本地程序，完全线上更新Hexo博客的方式，这样就可以在任意一台电脑上进行维护了，那么废话不多说，下面开始讲解方法。

需要用到的网站:

[【Travis CI】](https://www.travis-ci.org/)(点击进入，下同)：用于自动更新博客静态文件

[【GitHub】](https://github.com/)：用于存放Hexo博客源文件与静态文件

用到的软件：

[【GitHub Disktop】](https://desktop.github.com/)：用于更新博客源文件，由GitHub提供，自动部署搭建成功后，只需在本地安装GitHub就可以完全控制自己的Hexo博客，软件的使用不再此文章讨论范围内

<!-- more -->

##### 注册Github和搭建本地Hexo环境 #####
关于注册Github我之前发布过文章，【[点击这里](http://baipai.tk/2017/05/11/%E3%80%90%E5%8E%9F%E5%88%9B%E3%80%91%E5%B0%8F%E7%99%BD%E6%95%99%E4%BD%A0%E6%89%8B%E5%8A%A8%E6%90%AD%E5%BB%BAHexo%E5%8D%9A%E5%AE%A2%EF%BC%88Win%E7%89%88%EF%BC%89/)】可以查看注册和搭建Hexo方法。

##### 配置GitHub #####
登录GitHub，点击右上角头像进入【Settings】，依次选择【Developer settings】、【Personal access tokens】，然后点击【Generate new token】按钮创建密钥。选项按下图填写：

![图片1](/blog/images/【原创】使用Travis CI自动更新Hexo博客到Github/1.png)

注意：点击确定后，密匙只会显示一次，页面刷新后即隐藏，别忘了复制。

##### 配置Travis CI #####
Travis CI网站可以使用GitHub的帐号登录，登陆后自动关联GitHub中的仓库。界面如下：

![图片2](/blog/images/【原创】使用Travis CI自动更新Hexo博客到Github/2.png)

选择要存放Hexo博客源文件的仓库，点击左侧的开关将其激活（如上图），然后点击右侧的连接，进入下面界面：

![图片3](/blog/images/【原创】使用Travis CI自动更新Hexo博客到Github/3.png)

找到上图右侧标注方框的位置，点击选择【Settings】，打开如下界面：

![图片4](/blog/images/【原创】使用Travis CI自动更新Hexo博客到Github/4.png)

前面的配置按上图点选。

“Environment Variables”处填写前面在GitHub创建并复制的密钥，注意“GH_TOKEN”必须大写。

Travis CI部分配置完成。

##### 配置Hexo本地源文件 #####
按照最开始连接中的文章，你现在在本地应该已经建立好Hexo的本地程序并初始化了你的Hexo博客源代码。

进入你的Hexo博客源代码的根目录下，创建名为“.travis.yml”的文件，编辑内容如下：

```yml
language: node_js
node_js: stable

# S: Build Lifecycle
install:
  - npm install


#before_script:
 # - npm install -g gulp

script:
  - hexo g

after_script:
  - cd ./public
  - git init
  - git config user.name "name"             # 填写你的GitHub用户名
  - git config user.email "e-mail"          # 填写你的GitHub注册邮箱
  - git add .
  - git commit -m "Update docs"
  - git push --force --quiet "https://${GH_TOKEN}@${GH_REF}" master:master
# E: Build LifeCycle

branches:
  only:
    - master                                # 此处为源文件所在的仓库分支，默认master
env:
 global:
   - GH_REF: github.com/name/name.git       # 此处为静态文件仓库，也就是你设定GitHub Pages的仓库地址
```

注意修改上面代码中带有中文标注的地方。

接下来将Hexo博客源文件（包括“.travis.yml”文件）上传到你的GitHub用于存放源文件的仓库。

##### 完成 #####
至此配置完成，只要源文件仓库中的内容发生改变，Travis CI就会自动帮你更新Hexo博客的内容，你可以通过GitHub Disktop软件更新仓库中文件内容（如创建文章），也可以直接在网上手动创建、编辑MD文件，Travis Ci都会自动帮你更新你的Hexo博客的显示内容。