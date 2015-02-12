---
layout: plain
title: Windows Server 配置github服务器 一键同步服务器+版本控制
dec: Windows Server 配置github 服务器 实现编辑代码本地localhost访问，git版本控制，同步远端，远端见效果无缝衔接，不用再手工移动代码。
excerpt:  注意，我们安装ssh工具是因为win平台本身不支持SSH登陆和传输。如果是服
category: tech
exurl: http://www.cnblogs.com/liu946/
---
假期做一个web网站，搭建在win server 2003 的iis6上，是远端实体机目录在D:/www，我使用的开发工具是Mac osx 在 /Application /.../htdocs/www下。我想方便提交远端并能快速见到效果，前几次都是用scp，sftp等工具上传，效果不是很好，也不能和版本控制融合的很好。今天正好有时间，终于是到了解决的时候了。最终成果：实现编辑代码本地localhost访问，git版本控制，同步远端，远端见效果无缝衔接，不用再手工移动代码。

## 软件
- 环境：win server 2003 + IIS
(ps : 【IIS安装，与本文无关】在这里说一下，win server 2003 安装IIS出现的问题，IIS 安装提示缺少或者无法修复convlog.exe等文件的问题，这个问题是一个坑，虽然网上有各种此类文件下载，但是由于文件太多，还是推荐大家下载完整包[IIS官方下载|IIS 6.0 完整安装文件包最新免费下载](http://www.onlinedown.net/soft/472406.htm)）
- 新装软件：
 - 服务器端（win server 2003）
>copSSH 
git

 - 客户端（Linux，OS X）
>git

## 步骤
1. 下一步安装copSSH
 注意，我们安装ssh工具是因为win平台本身不支持SSH登陆和传输。如果是服务器使用UNIX Like 系统只安装git就可以了。这里SSH工具虽然说是一个传输协议工具，但是也不是只要是win平台的SSH工具都能使用，freesshd就不行。

 亲测，被坑，各种实验之后被告知这个软件并不能支持git的ssh传输，贴上freesshd死刑地址-协议错误。[git - fatal: protocol error: bad line length character: Unab - Stack Overflow](http://stackoverflow.com/questions/9661276/fatal-protocol-error-bad-line-length-character-unab)

2. 配置copSSH
 - copSSH的账户不能像FreeSSH那样自己在软件中定义，开启后就只能加注册用户和那个安装时设置的账户了。大家安装时就把这个配好就行。也可以之后在系统中添加账户。

 ![图片](http://img.blog.csdn.net/20140822225454296?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvY29kZV9zdHlsZQ==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
 - 上图，到这里的add就是选择用户了，并不能新建，如果想新建就去控制面板给windows新建用户吧。如图，设置密码登陆或是public key登陆，不怕麻烦每次输入密码，可以跳过下一步。

 我看网上一些人出现了不与配置文件不匹配问题，我的是匹配的，如果大家对勾不起作用可以试试改配置文件。<安装目录>\etc，ssh_config和sshd_config内容应该能看明白。

 ![图片](http://img.blog.csdn.net/20140822225312375?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvY29kZV9zdHlsZQ==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
 - 上图，（借用），再次提醒，特别注意。这里的add没有用，直接进入COPSSH安装目录下的home\<你选的user>\.ssh目录，打开authorized_keys文件（没有的别担心，新建一个，记事本打开），将客户端公钥，粘贴进来，保存，退出。（如何生成客户端公钥，参见概念）

 - 重启copssh，就是把setting那个绿灯按红再按绿。

 - 尝试登陆 
 Linux客户端：调出terminal
```
ssh <user>@<ip:port>
```
 如果配置正确，提示输入密码或是publickey直接登陆。exit退出ssh。表明ssh配置成功。user区分大小写！

3. 安装git

 服务器，客户端都要安装，下一步安装即可。

3. 新建项目

 声明一下，提倡使用服务器建立工程客户端clone的模式，这样新建项目可以很好地保存remote的地址，防止自己填入的地址出错。

 - win服务器
 新建工程文件夹，右键，git init here ，可以试着新建一个文件提交一次（如果新装的git记得配置git config中的用户名和邮箱），试一下git。（如果linux服务器的话使用terminal，不赘述）

4. clone到客户端

 - git clone 本身默认使用ssh协议，可以不写，也可以
```
git clone ssh://user@server:project.git
```
 - 那么主要问题就是路径名是啥的问题了。Win系统路径在UNIX like上的映射一直就是问题，也由于软件不同用法也不尽相同。如果使用我如上的配置，路径经测试如下。
 - 相对的 . 路径是在<安装目录>/home/<username>下，/是<安装目录>。
如果你的工程文件夹叫project.git在<安装目录>/home/<username>下，project.git文件夹又git init好了的话，就可以使用如下命令。
```
 git clone <user>@<server>:project.git
```
 - 绝对的，如果工程文件是D盘下的www文件夹的话使用：
```
git clone <user>@<server>:d:/www
```

5. 本地添加到github图形界面app
 Mac OS X 下的github直接按左上角加号，add，选择路径添加。如果你的工程是一个网站，你也可以选择先把项目放到htdocs文件夹下再添加到github.app中这样就可以边编辑边看结果，边提交，边同步远端了。这就是我一开始想要的效果。

6. 设置远端git仓库
 编辑完，提交时会出现一个错误。不能提交到远端当前分支，之后会解释，解决办法是，按照提示修改，在远端仓库下右键-git bash
```
git config receive.denyCurrentBranch ignore
```

7. 设置钩子自动将提交写入仓库文件中
 如果只是使用git服务器同步客户端之间的代码，那么已经完全够用了。但是如果你是使用远端当服务器，你想看到实时的变化，只push上去是不行的。
参考如下钩子用法，这个写的挺详细，之后有可能我也会写一个详细的研究：
[git推送到服务器自动同步到站点目录 - Carlton.C.X.Z的个人页面 - 开源中国社区](http://my.oschina.net/cxz001/blog/194196)


## 概念

1. git没有客户端服务端概念，就是从一个实体仓库推送到另一个实体仓库，把一个仓储中的commit同步到另一个仓库的.git文件夹而已，并没有修改远程仓库的代码，所以需要7步骤。而且显然一个仓库的提交是不能让其他人在正在编辑的分支上插队的。所以会出现最后的不让修改current的branch的情况。
