title: 小白教你手动搭建Hexo博客（Win版）
author: 无知の人
tags:
  - Hexo
categories:
  - 研究
date: 2017-05-11 18:29:00
origin: true
---
做为不懂技术的我，深深体会到对于使用电脑只会鼠标左右键的小白搭建Hexo博客的难处，所以我打算将网上所搜集的资料结合自己安装过程中所遇到的坑，整理出来分享给大家~

Ps.本教学仅限于Windows版本安装Hexo博客，其他系统请自行百度其他安装教程。

##### Hexo博客介绍

（不想了解Hexo的运作方式可以直接跳过此部分阅读安装方法）

文档类的说明我就不再重复了，想了解的朋友可以通过【[点击这里](https://hexo.io/zh-cn/docs/#什么是-Hexo？ "什么是-Hexo？")】查看官方介绍。

Hexo搭建的运行环境和安装步骤为：

> Windows（或其他系统） > Git + Node.JS > 【Hexo】 And 【Hexo相关插件】（如Hexo-Admin-QINIU）

那么我说说我对Hexo的理解吧，大家都熟知的系统是Windows，这是我们使用软件的常用平台，可以在上面聊QQ、发微博等操作，那么可以这么理解，Windows系统为我们使用一些常用软件的基础系统，如果你正在看我的这篇文章，说明你应该已经具备这样一个系统了。接下来就是Git和Node.JS工具（也可以称为软件），不要看名字觉得很陌生，其实他们和QQ等软件并无区别，都是需要一个系统（如Windows）来运行，只是使用起来会复杂一些，不过对于使用Hexo博客系统来说，只要简单了解就可以了。Git和Node.JS是使用Hexo博客的基础软件，比如我们没有浏览器就无法发微博，看网页是一个道理。安装以上两个软件后就可以使用我提供的方法安装Hexo博客和一些附属使用插件了，当然安装他们的方法我会在下面进行讲解。可能我说的比较笼统，但是Hexo博客的安装和使用其实就是这么简单！

<!-- more -->

##### 开始安装Hexo博客

**一、安装Git和Node.JS**

【安装Git】

Git是一种通用管理工具，界面类似Dos，不过操作方式很像Linux。

1.下载Git软件

首先我们需要下载Git安装程序，如果你对你的网络比较自信可以到【[官网](https://git-scm.com/download/win "官方下载地址")】进行下载。由于国内某些人为因素造成速度慢或无法下载的，可以【[点击这里](https://github.com/waylau/git-for-win "其他下载地址")】选择你所需要的版本，不过我建议下载最新版本。

2.安装Git软件

我当时没有按照教学做，直接是“下一步”装的，之后也没有出现问题，我安装的是最新的X64版本，如果担心出问题就【[点击这里](http://www.cnblogs.com/monodin/p/3268679.html "Git安装教学")】查看安装步骤，或者你和我一样心大就……下一步……下一步……吧~

3.测试安装

安装完成后在命令行（CMD）中输入：

```cmd
git –version
```

如果提示版本号，如下：

> git version 1.9.5. msysgit. 1

则说明已经成功安装了Git软件。

注：我所看得教学中安装时有一些设置，不过我全部默认选择也可以正常使用，所以我觉得可能是版本原因，最新的安装程序应该是选择默认就可以了。

【安装Node.JS】

1.下载Node.Js软件

可以直接【[点击这里](https://nodejs.org/en/ "官方下载地址")】在官方进行下载。

2.安装Node.JS软件

同Git的安装一样，点击“下一步”直到“完成”就可以了。

3.测试安装

在命令行中输入：

```cmd
node -v
```

看到如下提示，说明安装成功！

> v4.4.0

**二、本地安装Hexo博客程序**

接下来需要使用到前面所安装的Git软件，基本是由命令来完成的，不过不用担心，只要按照我所说的一步步的操作，用不了多久就可以使用上Hexo了。我还会在后面将Hexo安装过程中所遇到坑的解决办法和Hexo的基本使用操作一并奉上，所以请准备使用Hexo博客的小伙伴耐心的看下去哦~

Node.js安装完成后,在电脑任意位置，右键选择GitBash，执行npm命令：

```npm
npm install -g hexo
```

完成Hexo博客基础程序的安装。

然后在本地（建议最后一个盘根目录）创建HexoFile文件夹（名称可自定义），进入这个文件夹，右键选择GitBash，执行hexo命令：

```hexo
hexo init
```

这一步是对hexo进行初始化，然后执行：

```hexo
hexo install
```

安装Hexo博客的依赖包。

进行到这里，前面创建的HexoFile文件夹中应该已经生成了一些东西，而这个文件夹就是我们发布博客文章所需要的“大本营”。

接下来再执行：

```hexo
npm install hexo-server –save
```

可以将这个理解为安装一个hexo博客的预览插件，通过这个插件可以实现在本地查看你的Hexo博客页面。

现在你已经可以在本地查看你的Hexo博客了，先执行：

```hexo
hexo g
```

生成本地静态文件，再执行：

```hexo
hexo s
```

启动本地预览，执行完上面命令，会提示：

> INFO  Start processing
> INFO  Hexo is running at http://localhost:4000/. Press Ctrl+C to stop.

这时你可以打开浏览器，输入上面给出的地址“[http://localhost:4000](http://localhost:4000 "本地预览地址")”，一个全新的Hexo博客便呈现在你眼前了，是不是优点小激动呢！不过别着急，现在的Hexo博客因为只放在你的电脑中，所以只有你能看到，下一节我将介绍如何将Hexo博客系统生成的页面传送到Github上，让全世界都可以看到你！

**三、Github注册和使用**

【创建Github仓库】

1.注册Github账户

注册地址【[点击此处](https://github.com/join?source=header "注册地址")】，注册步骤比较简单在此就不详述了，如果有不懂的朋友可以【[点击这里](http://wiki.jikexueyuan.com/project/github-basics/sign-up.html "注册流程")】查看注册流程。

2.创建仓库（也就是我们需要存放Hexo博客页面的地方）

* 登陆你刚刚注册的帐号

* 点击右上角头像左侧的“+”号，选择“New repository”

* 在打开的新页面中依次填写下面项

 * Repository name：填写和你的用户名一致

 * Description：描述，可以随便写点什么
 
 * Public：点击选择这一项

 * Initialize this repository with a README：这一项必须勾选，否则后面可能无法继续进行
 
 * 点击Create repository完成创建，完成后会自动跳转到仓库
 
* 在上面右侧找到Settings选项，点击打开

* 在新页面中，将滚动条拉到最下方，找到GitHub Pages，点击Source中的下拉列表，选择master branch，并点击save保存

至此，最后一步操作的地方应该出现一个如“xxx.github.io”的地址，这个就是将来Hexo博客的浏览主页，当然如果拥有自己的域名可以与博客进行绑定，这个我后续会介绍到。

【配置SSH密匙】

配置SSH密匙的好处，就是在本地通过Git对Github的仓库进行操作时不用重复输入密码进行验证，Github会记住你配置了SSH密匙的电脑，就像QQ登陆时记住密码一样。或者你也可以下载Github的桌面工具，可以更方便的对仓库进行管理而无需配置密匙。

> 小贴士：Git属于管理系统，而Github是一个可以用Git软件进行操作的网上代码仓库，虽然二者名字很像，但是Git并不是由Github公司开发的，许多其他网上的代码托管仓库都可以使用Git进行管理。

下面开始配置SSH密匙。

1.检查电脑中是否有已存在的密匙，步骤如下：

 * 在任意目录打开Git Bash界面（右键任意目录空白处可选择启动）
 
 * 执行 `ls -al ~/.ssh` 命令查看是否有以存在的密匙，默认的密匙名称为下列之一
 
  * id_dsa.pub
  * id_ecdsa.pub
  * id_ecdsa.pub
  * id_ecdsa.pub
  
对于第一次安装的用户来说，应该不会存在已有密匙。

2.创建新的密匙

* 输入 `ssh-keygen -t rsa -b 4096 -C "email@example.com"` (邮箱处使用你自己的地址）

* 当出现如下字样时，按回车将密匙保存在默认地址

 * > Enter a file in which to save the key (/Users/you/.ssh/id_rsa): [Press enter]

* 接下来会如下提示输入安全密码，可以为空，不过安全起见我是选择输入了（输入密码时是隐藏的没有任何提示）

 * > Enter passphrase (empty for no passphrase): [Type a passphrase]  
  > Enter same passphrase again: [Type passphrase again]

* 输入 `eval "$(ssh-agent -s)"` 确保ssh-agent启用

* 输入 `$ ssh-add ~/.ssh/id_rsa` 命令将密匙添加到ssh-agent

至此，新的密匙创建完毕！

3.将创建的密匙添加到Github

要配置GitHub的帐户需要使用新的SSH密钥，你需要将其添加到你的帐户GitHub中。

* 执行`clip < ~/.ssh/id_rsa.pub` 命令（如果文件名不对，使用上面的方法查看你已存在的密匙）后，密匙复制到你的剪贴板中

* 打开Github页面登录你的帐号，点击头像，选择“Settings”

* 在用户设置栏中，点击“SSH keys”，然后点击“New SSH key”

* 在添加密匙界面中Title为你自己为密匙起的名字，在下面key出粘贴剪贴板中的密匙

* 点击“ADD SSH key”完成添加

可以在Git Bash界面中输入 `ssh -T git@github.com` 命令来测试密匙是否添加成功。系统会返回如下信息：

> The authenticity of host 'github.com (192.30.252.1)' can't be established.
RSA key fingerprint is 16:27:ac:a5:76:28:2d:36:63:1b:56:4d:eb:df:a6:48.
Are you sure you want to continue connecting (yes/no)?

输入“yes”回车，如果系统提示如下：

> Hi username! You've successfully authenticated, but GitHub does not
provide shell access.

说明密匙配置成功！

**四、配置Hexo关联Github帐号**

1.打开刚才建立的HexoFile文件夹，找到名为“_config.yml”的文件，用你喜欢的编辑器将其打开，然后将滚动条拖至最下方，找到“deploy”这里，按如下输入

> deploy: 
> 　type: git 
> 　repository: https://github.com/xxx/xxx.github.io.git 
> 　branch: master

这里有几个坑需要注意：

* deploy下面的三行必须有至少两个英文空格的缩进，而deploy不用缩进

* 冒号“：”后面必须要有一个空格，只有前面的需要加空格，后面的例如网址中的不需要

* 从Hexo3版本开始，type配置要填写git而不是github，有些旧的教学会使用github，应改成git

* 将示例中的xxx修改为你的github仓库地址，可以在网站登录用户查看

将上面文件配置好后保存，然后打开HexoFile文件夹，在文件夹中右键打开Git Bash。

> 注意：一定要在HexoFile文件夹下打开，否则需要手动定位此目录，只有定位到这个目录下才可以使用Hexo命令。

在Git Bash中执行如下命令：

```hexo
hexo g
```

用来生成网站静态文件，然后输入：

```hexo
hexo d
```

来将生成的静态页面上传到Github中。

> 小贴士：第一次执行 `hexo d` 时会让你输入你的Github帐号和密码，之后再上传时无需输入

完成上面操作后，就可以使用前面得到的地址“xxx.github.io”来登录你的公共页面了，这个页面是所有人都可以看到的。至此，Hexo的基本配置和网络发布功能就都已完成了，可以开始你的Hexo之旅了！下面将介绍绑定域名的操作，有需要继续往下看吧~

**五、绑定自己的域名**

Github提供绑定域名的功能，并且操作非常简单。

首先在你的Github的仓库中创建“CNAME”文件，编辑内容为你需要绑定的域名。

> 注意：
> 　1.文件名“CNAME”必须大写，并且没有后缀名
> 　2.内容为你要绑定的域名，如：www.baidu.com（不含http://和其他/符号）

现在Github这边就已经设置好了，然后进入你的域名管理界面，添加新的CNAME，并将地址指向你之前的Github地址。

> xxx.github.io

现在你的域名就完成绑定Github了，如果页面打不开不要着急，一般等待5~10分钟后就可以正常访问了。

> **大功告成，现在你已经拥有自己的Hexo博客了！似拔似很简单^ ^**