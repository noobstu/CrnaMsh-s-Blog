---
layout: article
title: 从零开始的jekyll+Github pages搭建博客
tags: 教程 博客 Jekyll Github-Pages ruby
---


## 前言&瞎扯

本人目前还是萌新，在群里看到大佬的博客，哇！瞬间眼睛放光那是。于是借着前人栽下的树自己也来做点教程www
所以，大家好啊，今天来点大家想看的东西啊
    
先放个我的参考教程在[这里](https://megamu.icu/2016/10/jekyll_tutorials1/#%E4%BF%AE%E6%94%B9%E6%88%90%E4%BD%A0%E8%87%AA%E5%B7%B1%E7%9A%84%E5%8D%9A%E5%AE%A2)，我会尽量多讲一点东西

由于我目前只用过Windows系统，所以只有Windows的教程，对母鸡啦Mac的用户们
不过你也许可以参考一下以下的步骤
>安装 Xcode 和 Command-Line Tools。下载方式 Preferences → Downloads → Components



## ***1.介绍***
   
　　Jekyll 是一个简单的博客形态的静态站点生产机器。它有一个模版目录，其中包含原始文本格式的文档，通过 Markdown （或者 Textile） 以及 Liquid 转化成一个完整的可发布的静态网站，你可以发布在任何你喜爱的服务器上。Jekyll 也可以运行在 GitHub Page 上，也就是说，你可以使用 GitHub 的服务来搭建你的项目页面、博客或者网站，而且是完全免费的

　　Jekyll 是一个免费的简单静态网页生成工具，可以配合第三方服务例如： Disqus（评论）、多说(评论) 以及分享 等等扩展功能，Jekyll 可以直接部署在 Github（国外） 或 Coding（国内） 上，可以绑定自己的域名。
　　
　　Jekyll 的核心其实是一个文本转换引擎。它的概念其实就是： 你用你最喜欢的标记语言来写文章，可以是 Markdown，也可以是 Textile,或者就是简单的 HTML, 然后 Jekyll 就会帮你套入一个或一系列的布局中。在整个过程中你可以设置URL路径, 你的文本在布局中的显示样式等等。这些都可以通过纯文本编辑来实现，最终生成的静态页面就是你的成品了。

一个基本的 Jekyll 网站的目录结构一般是像这样的：
```
.
├── _config.yml
├── _includes
|   ├── footer.html
|   └── header.html
├── _layouts
|   ├── default.html
|   ├── post.html
|   └── page.html
├── _posts
|   └── 2016-10-08-welcome-to-jekyll.markdown
├── _sass
|   ├── _base.scss
|   ├── _layout.scss
|   └── _syntax-highlighting.scss
├── about.md
├── css
|   └── main.scss
├── feed.xml
└── index.html
```
这些目录结构以及具体的作用可以参考以下的文档
　　以下为最重要的一些参考文档,遇到问题可以先看看哦，特别是第三个GitHub Docs。也请别忘了Google百度一下: [Jekyll中文文档](https://www.jekyll.com.cn/)、[Jekyll英文文档](https://jekyllrb.com/)、[Jekyll&GitHub Pages文档](https://docs.github.com/cn/pages/setting-up-a-github-pages-site-with-jekyll/testing-your-github-pages-site-locally-with-jekyll)。



## ***2.环境安装***
### **安装ruby环境**
点开这个链接[Ruby](http://www.ruby-lang.org/en/downloads/)
看到Ways of Installing Ruby这栏，根据不同的操作系统选择不同的方式安装Ruby（想要学习源码也可以在下面下载）

### **安装RubyGems**
点开这个链接[RubyGems](https://rubygems.org/pages/download)
下载压缩包，解压后运行setup.rb

### **安装Git Bash**
对于git环境的配置，为了方便部署到远端服务器
[git Bash安装](https://git-scm.com/download/win)
下载对应版本后运行~
具体的安装操作可以看[这个](https://blog.csdn.net/weixin_43951315/article/details/104921428?spm=1001.2101.3001.6661.1&utm_medium=distribute.pc_relevant_t0.none-task-blog-2%7Edefault%7ECTRLIST%7Edefault-1-104921428-blog-83032408.pc_relevant_default&depth_1-utm_source=distribute.pc_relevant_t0.none-task-blog-2%7Edefault%7ECTRLIST%7Edefault-1-104921428-blog-83032408.pc_relevant_default&utm_relevant_index=1)

 *注意：学到配置ssh就可以了，关于push代码的部分，后续会提到，与教程中的方法并不一致*

### **安装Jekyll环境**
 打开cmd，输入以下指令

```
$ gem install bundler
$ bundle install
$ gem install jekyll
```
 这样就完成啦
 


## ***3.搭建步骤***
### **1.在github创建远端仓库**

在任何gtihub页面的右上角，使用 +下拉菜单选择 New repository（新建仓库）

[![jNsnKO.png](https://s1.ax1x.com/2022/07/05/jNsnKO.png)](https://imgtu.com/i/jNsnKO)

使用 Owner（所有者）下拉菜单选择你想要拥有仓库的帐户。
[![jNssGq.png](https://s1.ax1x.com/2022/07/05/jNssGq.png)](https://imgtu.com/i/jNssGq)

输入仓库的名称和说明（可选）。 
前面起一个好听的名字，但是最后一定要以github.io结尾
[![jNyXcV.png](https://s1.ax1x.com/2022/07/05/jNyXcV.png)](https://imgtu.com/i/jNyXcV)

选择仓库的可见性
简单来讲，看你个人喜好就好
[![jN6eBD.png](https://s1.ax1x.com/2022/07/05/jN6eBD.png)](https://imgtu.com/i/jN6eBD)

### **2.创建本地的博客**
现在本地随意一个位置创建一个文件夹，作为你的博客在本地的仓库
在刚刚创建的文件夹里打开终端
使用`jekyll new`来创建你的本地博客
```
$ jekyll new myblog
# myblog 为示例可以替换成你自己的博客名字
```

打开Jekyll创建的gemfile文件（打开方式选择记事本等等）

将 "#" 添加到以 `gem "jekyll "` 开头的行首，以注释此行

编辑以 `# gem "github-pages"` 开头的行来添加 `github-pages` gem。 将此行更改为：
```
gem "github-pages", "~> GITHUB-PAGES-VERSION", group: :jekyll_plugins
```
关于版本依赖项等细节可以查看之前的Github pages文档

恭喜你，你已经做好所有搭建博客的准备了
接下来就是在本地进行测试（可以跳过此步骤，但是不建议），随后push到你的远端上
### **3.在本地通过Jekyll测试**
在你刚刚创建了博客的文件里用终端打开

[![jat1Xj.png](https://s1.ax1x.com/2022/07/06/jat1Xj.png)](https://imgtu.com/i/jat1Xj)

运行
```
$ jekyll serve
```
如果提示
>Server running... press ctrl-c to stop.

说明你的博客已经成功在本地运行了！
只要在浏览器中输入`http://localhost:4000`就能看见你博客的样子了
虽然还只是一篇空白，但是没关系，接下来会讲到如何美化和上传你的博客文章

当然，如果你没有成功运行，请注意弹出的报错，极有可能是有一些依赖项没有安装（版本不对），自行安装或更新后应该问题也不大了

### **4.将博客push到Github上**

首先，在配置好git bash之后用git bash打开刚刚的文件夹
即在文件夹里右键→git bash here
[![jNWO39.png](https://s1.ax1x.com/2022/07/05/jNWO39.png)](https://imgtu.com/i/jNWO39)

接下来在git bash里执行以下代码
```
$ git init 
#在本地目录里设置你的仓库

```
下一步
```
git add .
$ git commit -m'这里写上提交备注'
$ git remote add origin https://github.com/USER/REPOSITORY.git
#将https://github.com/USER/REPOSITORY.git你的仓库网址
$ git push -u origin BRANCH
#将BRANCH替换为你操作的分支，master为主要分支
```
等待一段时间，打开你的仓库页面，你就可以看到你的博客已经成功push到了Github上

点击`Settings`，选中Pages，就可以看到你的博客页面啦
[![jdSMiF.png](https://s1.ax1x.com/2022/07/06/jdSMiF.png)](https://imgtu.com/i/jdSMiF)



## ***4.博客美化***
说到博客美化，那自然是对于博客主题的选择（其实也可以自己写，请大佬开始你的表演）

关于主题的选择自然多种多样，一般大佬都很愿意开放自己的博客源码
复制下来慢慢的像修忒斯之船改成你自己的就行了
例如想要使用和我一样的模板可以点击最下方的`TeXt Theme`记得多支持大佬

我这里提供几种方法
一个可以在之前的pages页面，点击`Choose a theme`里面可以看到许多Github提供的主题

[![jdpyp4.png](https://s1.ax1x.com/2022/07/06/jdpyp4.png)](https://imgtu.com/i/jdpyp4)

或者也可以看这个 [Jekyll主题列表](http://jekyllthemes.org/)
里面有很多可以自定义的博客模板
选一个你喜欢的吧

## ***5.撰写博客文章***
　　所有的文章都是 _posts 目录下面，文章格式为 markdown 格式，文章文件名可以是 .markdown 或者 .md。

　　编写一篇新文章很简单，你可以直接从 _posts/ 目录下复制一份出来 2016-10-16-welcome-to-jekyll副本.markdown ，修改名字为 2016-10-16-article1.markdown ，注意：文章名的格式前面必须为 2016-10-16- ，日期可以修改，但必须为 年-月-日- 格式，后面的 article1 是整个文章的连接 URL，如果文章名为中文，那么文章的连接URL就会变成这样的：http://leopardpan.cn/2015/08/%E6%90%AD%E5/ ， 所以建议文章名最好是英文的或者阿拉伯数字。 双击 2016-10-16-article1.markdown 打开
```
---
layout: post
title:  "Welcome to Jekyll!"
date:   2016-10-16 11:29:08 +0800
categories: jekyll update
---

正文...

```
title: 显示的文章名， 如：title: 我的第一篇文章
date: 显示的文章发布日期，如：date: 2016-10-16
categories: tag标签的分类，如：categories: 随笔

注意：文章头部格式可以依据你选择的主题不同而不同
{:.warning}

关于markdown格式的语法可以参考[Cmd Markdown 编辑阅读器的教程](https://www.zybuluo.com/mdeditor#)


## 6.后记
本文只提供了最基本的搭建博客方法和使用方法
你说其他例如评论功能？
可以参考[这个](https://waliblog.com/jekyll/2017/11/21/jekyll(1).html)
当时看到这个真的觉得白写了www

你就当我写的比较详细吧，人人的情况都不同，方法也不尽相同，请善用百度，或者我以后开了评论的功能可以问我？（我很菜啦，估计没法回答）

大概就这样了，这是我写的第一篇博客，就多说点东西吧，因为偷懒等等原因，目前不少部分是东拼西凑起来的，就当整合包看吧，怎么说我不是博客的生产者，我只是博客的搬运工（）

大概有时间会改善的，加点自己的东西上去，但是初版就这样了，我还有好多东西要学习
[![jdSWFS.png](https://s1.ax1x.com/2022/07/06/jdSWFS.png)](https://imgtu.com/i/jdSWFS)

来张壁纸怎么样（
[![jdP3tK.jpg](https://s1.ax1x.com/2022/07/06/jdP3tK.jpg)](https://imgtu.com/i/jdP3tK)
~~紫苑我真的好喜欢你啊，为了你我要玩东方凭依华~~

咳咳
# ***the end***
