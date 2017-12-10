---
title: 基于Github和Hexo搭建博客
copyright: true
top: 9ß
date: 2017-08-13 19:02:26
tags: Hexo
categories: 搭建博客
password:
---



<!-- 标签别名 -->
{% cq %}优秀的人，不是不合群，而是他们合群的人里面没有你 {% endcq %}

正常都应该讲一讲为什么搭建博客，不过既然您能看见这篇文章，就说明你想搭建一个自己的博客，无论自己记录自己的东西，或是为了显得高大上。那就不废话了，进入正题。

其实教大家搭建博客的文章很多，讲的都不错，本来不打算写的，不过既然搭建了，正好刚学会就换了个电脑，还需从头搭建一边，就顺便写个记录下，权当第一篇博客了。正式进入正题，哈哈哈哈哈！！！

我的博客是基于github和hexo搭建的，至于为什么这么配置呢？网上这个教程很多，so...你晓得。在这里要非常感谢[吴小龙同学](http://wuxiaolong.me/)的[手把手教你建github技术博客by hexo](http://wuxiaolong.me/2015/07/31/build-blog-by-hexo/),差不多就是按照他的这个文章，搭建起来的。
<!--more-->
# 第一步 环境准备

## 安装 Git
用来将本地Hexo内容提交到Github上。
### windows系统的：

下载 [msysgit](http://msysgit.github.io/) 并执行即可完成安装。

### MAC：
如果有Xcode，自带Git。如果没有Xcode可以参考[Hexo官网](https://hexo.io/docs)上的安装方法。也可以通过在这里下载[git](https://git-scm.com/download/mac),我是通过[git](https://git-scm.com/download/mac)下载的，安装的时候不要双击来安装，不会的可以参考[mac 上安装git步骤及注意事项](http://blog.csdn.net/helinlin007/article/details/50358633)。


## 安装Node.js
要使用hexo，需要先下载[Node.js](https://nodejs.org/en/)，选择左边的就好了，然后一路安装。
![Node.js](http://upload-images.jianshu.io/upload_images/1492631-869336da616cf7f4.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## 安装Hexo

利用 npm 命令即可安装。

### windows：

在任意位置点击鼠标右键，选择Git bash
```
npm install -g hexo
```
问题:
npm ERR! registry error parsing json 错误
可能需要设置 npm 代理，执行命令
```
npm config set registry http://registry.cnpmjs.org
```
hexo:command not found
删除刚刚安装的 npm 目录，重新执行命令：
```
npm install -g hexo
```
来安装 hexo。

### mac

终端执行如下命令：
```
$ sudo npm install -g hexo
```
输入管理员密码（Mac登录密码）即开始安装 (sudo:linux系统管理指令
>注意坑一：[Hexo官网](https://hexo.io/docs)上的安装命令是$ npm install -g hexo-cli
，安装时不要忘记前面加上sudo
，否则会因为权限问题报错。

# 初始化HEXO-搭建本地博客

## windows
安装完成后，在你喜爱的文件夹下（如 H:\hexo），执行以下指令(在 H:\hexo 内点击鼠标右键，选择 Git bash)，Hexo 即会自动在目标文件夹建立网站所需要的所有文件。
```
hexo init blog
```
blog是你建立的文件夹名称
安装依赖包
```
npm install
```
## mac:

终端cd到一个你选定的目录，执行hexo init命令：
```
$ hexo init blog
```
blog是你建立的文件夹名称。cd到blog文件夹下，执行如下命令，安装npm：
```
$ npm install
```
**本地博客就搭建好了！！！！！**  
执行如下命令，开启hexo服务器：
```
hexo generate
hexo server
```
此时，浏览器中打开网址[http://localhost:4000](http://0.0.0.0:4000/)，能看到如下页面

![image.png](http://upload-images.jianshu.io/upload_images/1492631-f18827220cfcecb9.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/640)
**问题:**
执行 hexo server 提示找不到该指令
解决办法：
在 Hexo 3.0 后 server 被单独出来了，需要安装 server，安装的命令如下：
```
npm install hexo -server --save
```
安装此 server 后再试，问题解决
# github配置
## 注册账号
[https://github.com/](https://github.com/)
![image.png](http://upload-images.jianshu.io/upload_images/1492631-14d914fed7f84f4a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/640)
输入账号、邮箱、密码，然后点击注册按钮.然后去验证下邮箱
## 创建页面仓库
这个仓库的名字需要和你的账号对应，格式: yourname.github.io

![image.png](http://upload-images.jianshu.io/upload_images/1492631-8c61084f0acedc64.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/640)

![image.png](http://upload-images.jianshu.io/upload_images/1492631-85fc66b467c3f847.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/640)
创建之后在浏览器中输入yourname.github.io,比如我的[https://songlma.github.io](https://songlma.github.io)

![image.png](http://upload-images.jianshu.io/upload_images/1492631-b1b10a79cceab3c5.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/640)

备注：只有你仓库名称安装对应格式才可以直接通过 yourname.github.io访问，当然如果你打算用自己的域名绑定github的话，这个仓库名称就随便了，后面会讲到怎么绑定个人域名。
# 本地的hexo与github关联起来。
## 生成SSH文件
github是通过配置ssh来验证身份的。至于什么是ssh，不知道的大家自行百度吧。
先检验电脑中是否有ssh：
```
ls -al ~/.ssh
```
如果有文件id_rsa.pub或id_dsa.pub，将SSH key添加到Github中。没有的就先生成

执行如下命令生成public/private rsa key pair，注意将your_email@example.com换成你自己注册Github的邮箱地址。
```
ssh-keygen -t rsa -C "your_email@example.com"
```
按 3 个回车，密码为空。

ssh文件地址：  

**windows:** C:\Users\Administrator.ssh 下，得到两个文件 id_rsa 和 id_rsa.pub。

**mac:** Find前往文件夹~/.ssh/id_rsa.pub

**在 GitHub 上添加 SSH 密钥**
打开id_rsa.pub文件，里面的信息即为SSH key，将这些信息复制到Github的[Add SSH key](https://github.com/settings/keys)页面即可。

关于配置多个ssh文件请参考[同一个Mac，配置多个SSH Key](http://shinancao.github.io/2016/12/18/Programming-Git-1/)

## Hexo配置
**目录结构**
```
├── .deploy       #需要部署的文件
├── node_modules  #Hexo插件
├── public        #生成的静态网页文件
├── scaffolds     #模板
├── source        #博客正文和其他源文件，404、favicon、CNAME 都应该放在这里
|   ├── _drafts   #草稿
|   └── _posts    #文章
├── themes        #主题
├── _config.yml   #全局配置文件
└── package.json
```
**全局配置 _config.yml**
```
# Hexo Configuration
# Docs: http://hexo.io/docs/configuration.html
# Source: https://github.com/hexojs/hexo/
# Site #站点信息
title:  #标题
subtitle:  #副标题
description:  #站点描述，给搜索引擎看的
author:  #作者
email:  #电子邮箱
language: zh-CN #语言

.......

theme: landscape-plus #主题
exclude_generator:
plugins: #插件，例如生成 RSS 和站点地图的
- hexo-generator-feed
- hexo-generator-sitemap
# Deployment #部署，将 lmintlcx 改成用户名
deploy:
 type: git
 repo: 刚刚github创库地址.git
 branch: master
```
注意：
配置文件的冒号“:”后面有一个空格   
repo: 刚刚 GitHub 创库地址.git    
type:值为git。
![image.png](http://upload-images.jianshu.io/upload_images/1492631-fd78caecb155c0c6.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

```
deploy:
  type: git
 repo: https://github.com/songlma/songlma.github.io.git
 branch: master

```
## hexo命令行使用

```
hexo help #查看帮助
hexo init #初始化一个目录
hexo new "postName" #新建文章
hexo new page "pageName" #新建页面
hexo generate #生成网页，可以在 public 目录查看整个网站的文件
hexo server #本地预览，'Ctrl+C'关闭
hexo deploy #部署.deploy目录
hexo clean #清除缓存

```
**强烈建议每次执行命令前先清理缓存，每次部署前先删除 .deploy 文件夹**   
简写:
```
hexo n == hexo new
hexo g == hexo generate
hexo s == hexo server
hexo d == hexo deploy
```
## hexo部署
执行下列指令即可完成部署。
```
hexo generate
hexo deploy
```
hexo deploy 问题：Deployer not found: git
```
npm install hexo-deployer-git --save
```
再重新 hexo deploy ，以下提示说明部署成功：
```
[info] Deploy done: git
```
代码就已经传到github上了

![image.png](http://upload-images.jianshu.io/upload_images/1492631-8a932d762ce9a3a1.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/640)

点击settings:往下拉到github pages

![image.png](http://upload-images.jianshu.io/upload_images/1492631-24bec0f302058f50.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
**点击链接，就到了你的博客了，基础的搭建完成了。**

# 绑定个人域名
## 域名的购买
购买域名我是在[GoDaddy官网](https://sg.godaddy.com/zh/)购买的，也可以也可以到[阿里万网](http://wanwang.aliyun.com/)购买。至于为什么是在在GoDady买呢？看见第一篇搭建博客就是在GoDady买的，so...
感谢[如何搭建一个独立博客——简明 GitHub Pages与 jekyll 教程](http://www.cnfeat.com/blog/2014/05/10/how-to-build-a-blog/)

![image.png](http://upload-images.jianshu.io/upload_images/1492631-be2ccddcde3e81b5.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
接下来要做的就是注册，登陆，挑选你想要的域名，加入购物车，GoDaddy 其他域名收费服务，不要管，继续「进入购物车」。
确认购买 修改购买年限，默认是两年，可以修改成 1/2/3/5/10 年，随自己喜欢。
如果你不是土豪，可以上网搜 [GoDaddy 优惠码](https://www.google.com/search?q=GoDaddy%20%E7%9A%84%E4%BC%98%E6%83%A0%E7%A0%81)，一般优惠幅度是 20%~ 30% 不等
填完之后，五年的费用就从 415.56 会变成 333.95 元。
我当时从手机浏览器打开的，直接有一个优惠码，大概优惠了20%多。
用支付宝结账，这个域名就是你的了。如果结算出现问题，可以[查看这个页面](https://www.dute.me/godaddy-alipay.html)。
>**注册时用户填写信息时一定要输入正确的邮箱名字，否则修改十分麻烦。
买完域名之后一定要记得去自己的邮箱查看激活邮件，否则域名激活不了。**  

购买成功的话在「我的账户 > 我的产品」

![image.png](http://upload-images.jianshu.io/upload_images/1492631-95318100d481fb72.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## 将独立域名与 GitHub Pages 的空间绑定
### DNS 设置

用 DNSpod，快，免费，稳定。
注册[DNSpod](http://www.cnfeat.com/blog/2014/05/10/how-to-build-a-blog/www.dnspod.cn)，添加域名，如下图设置。

![image.png](http://upload-images.jianshu.io/upload_images/1492631-b1244a2f8bbd4a7b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
其中 A 的记录指向的ip地址是 GitHub Pages 的提供的 ip
如何知道你的 GitHub 上项目的 ip，如下：

![image.png](http://upload-images.jianshu.io/upload_images/1492631-af5d181301e843c3.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
www 指定的记录是你在 GitHub 注册的仓库。
### 去 GoDaddy 修改 DNS 地址
更改 [GoDaddy](https://mya.godaddy.com/) 的 Nameservers 为 DNSpod 的 NameServers。

![image.png](http://upload-images.jianshu.io/upload_images/1492631-53af7a4a36bed992.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
**将 GoDaddy 的 Nameservers 更改成 f1g1ns1.dnspod.net 和 f1g1ns2.dnspod.net**
![image.png](http://upload-images.jianshu.io/upload_images/1492631-3f24810f6c5a3574.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

在/blog/themes/landscape/source目录下新建文件名为：CNAME文件，注意没有后缀名！直接将自己的域名如：songlma.com写入
>注意坑：网上许多都是说在Github上直接新建CNAME文件，如果这样的话，在你下一次执行hexo d部署命令后CNAME文件就消失了，因为本地没有此文件嘛。

再次执行
```
hexo g
hexo d
```
在浏览器输入你的个人域名例如：[http://songlma.com/](http://songlma.com/)

# HEXO样式
博客搭建成了，个人域名也绑定了，是不是觉得博客样式好丑！！！！！！！！！
不过hexo很强大，支持多种主题样式从[官方主题](https://hexo.io/themes/)挑选你喜欢的主题，

![image.png](http://upload-images.jianshu.io/upload_images/1492631-df5d371368d5ea18.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
拿NexT为例 ASdfg jk  c                     cvb mvc
点击上图的红框没复制主题地址，然后进入你的blog中themes目录，进入以下操作：
windows：可以直接进入文件夹，右键选择Git bash：
mac:在终端使用cd 命令进入：
```
git clone https://github.com/iissnan/hexo-theme-next.git（主题的地址）
```

![image.png](http://upload-images.jianshu.io/upload_images/1492631-58548d3b64025939.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
下载成功后themes文件下多出一个hexo-theme-next文件夹，next这是我改的名字

![image.png](http://upload-images.jianshu.io/upload_images/1492631-94fea7ace0327bf5.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

打开__config.yml文件，将themes修改为next（下载到的主题文件夹的名字）

![image.png](http://upload-images.jianshu.io/upload_images/1492631-a1598e61abdab53a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
 保存之后，在blog目录下，
  ```
hexo s
```
打开[http://localhost:4000](http://localhost:4000)主题就变成这个样子了。根据自己喜欢去选择自己的主题。
![image.png](http://upload-images.jianshu.io/upload_images/1492631-adfa04162c8a003f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

[NexT](http://theme-next.iissnan.com/getting-started.html)上面有详细的讲解，初次接触者建议先用着这个，等熟悉了，再换别的。


# 参考：
> 购买独立域名：[如何搭建一个独立博客——简明 GitHub Pages与 jekyll 教程](http://www.cnfeat.com/blog/2014/05/10/how-to-build-a-blog/)
> 主题相关[Hexo搭建博客教程](https://thief.one/2017/03/03/Hexo%E6%90%AD%E5%BB%BA%E5%8D%9A%E5%AE%A2%E6%95%99%E7%A8%8B/)
windows博客基本搭建[手把手教你建github技术博客by hexo](http://wuxiaolong.me/2015/07/31/build-blog-by-hexo/)
快速、简洁且高效的博客框架[hexo官网](https://hexo.io/zh-cn/)
mac博客基本搭建[Mac上搭建基于GitHub Page的Hexo博客](http://jeasonstudio.github.io/2016/05/26/Mac%E4%B8%8A%E6%90%AD%E5%BB%BA%E5%9F%BA%E4%BA%8EGitHub-Page%E7%9A%84Hexo%E5%8D%9A%E5%AE%A2/)
[next主题](http://theme-next.iissnan.com/)
[为NexT主题添加文章阅读量统计功能](https://notes.wanghao.work/2015-10-21-%E4%B8%BANexT%E4%B8%BB%E9%A2%98%E6%B7%BB%E5%8A%A0%E6%96%87%E7%AB%A0%E9%98%85%E8%AF%BB%E9%87%8F%E7%BB%9F%E8%AE%A1%E5%8A%9F%E8%83%BD.html#%E9%85%8D%E7%BD%AELeanCloud)

[备份Hexo博客源文件](https://notes.wanghao.work/2015-04-06-备份Hexo博客源文件.html)
[自动备份Hexo博客源文件](https://notes.wanghao.work/2015-07-06-%E8%87%AA%E5%8A%A8%E5%A4%87%E4%BB%BDHexo%E5%8D%9A%E5%AE%A2%E6%BA%90%E6%96%87%E4%BB%B6.html)

问题：hexo搭建的博客，怎么设置主页内容的高度（每篇博客就显示几行，点击标题时进入正文）？
写文章时插入
```
<!--more-->
```
,文章会自动从插入的位置截断，也就是说在博客中只显示
```
<!--more-->
```
之前的内容，点击阅读全文之后会显示所有内容。

> 再次感谢[吴小龙同学](http://wuxiaolong.me/)
