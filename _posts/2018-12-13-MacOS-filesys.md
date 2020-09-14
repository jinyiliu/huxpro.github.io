---
layout:		post
title:		"MacOS 系统文件详解"
subtitle:	"了解自己电脑的第一步"
date:		2018-12-13 12:00:00
author:		"Jinyi"
header-img:	"img/post-bg-unix-linux.jpg"
catalog:	true
tags:
    - Mac
---

有点好奇，所以做了一些小调查。

### root/files

- **Applications** 安装的软件
- **Library** 系统资源库，包括数据文件、帮助文件、文档等等
- **Network** 网络节点存放目录
- **System** 包含由 Apple 安装的系统软件，其所包含的文件夹只有`Library`和`iOSSupport`
- **Users** 用户文件夹，其中`Guest`是访客文件夹，`Shared`是共享文件夹，`liujinyi`是我的文件夹
- **Volumes** 文件系统挂载点存放目录，这个文件夹中其实只有一个链接`Macintosh HD -> /`
- **bin** 传统 unix 系统命令（unix-style binaries）的存放目录，如常见的`ls`、`chmod`、`expr`、`cat`、`df`、`pwd`、`rm`、`mv`、`echo`、`cp`、`link`、`ln`、`mkdir`、`rmdir`等
- **cores** 内核转储文件存放目录，当一个进程崩溃时，如果系统允许则会产生转储文件
- **dev** device 的缩写，设备文件的存放目录，设备被当成文件，这样以来设备被抽象化，便于读写、网络共享以及需要临时装载到文件系统中，如果使用`ls -l`查看，会发现`dev`中的文件的类型通常是**块设备文件**`b`和**字符设备文件**`c`
- **etc** 此目录实际为指向`/private/etc`的链接，是标准 unix 系统配置文件存放目录，是系统中最重要的目录之一，这个目录下存放了系统管理时要用到的各种配置文件和子目录，我们要用到的网络配置文件、文件系统、设备配置信息、设置用户信息等都在这个子目录下，如用户密码文件`/etc/passwd`
- **home** 用户主目录，Mac 下默认为空
- **installer.failurerequests** [stackexchange - What is installer.failurerequests in the root directory?](https://apple.stackexchange.com/questions/229604/what-is-installer-failurerequests-in-the-root-directory)
- **net** 
- **private** 里面的子目录存放了`/tmp`、` /var`、` /etc`等链接目录的目标目录
- **sbin** 超级用户（Super user bin）使用的传统 unix 系统管理类命令（unix-style binaries）存放目录，如`fdisk`、`ifconfig`、`ping`、`dump`、`init`等
- **tmp** 临时文件存放目录，其权限为所有人任意读写，此目录实际为指向`/private/tmp`的链接
- **usr** 是系统中最重要的目录之一，通常这一文件系统很大，因为所有程序都安装在这里
- **var** 存放经常变化的文件，如日志文件，此目录实际为指向`/private/var`的链接

### root/.hidden_files

- **.DS_Store** 见「个人目录文件」中的相关条目
- **.Trashes** 垃圾桶
- **.file**
- **.vol**
- **.Spotlight-V100** 是 Spotlight 所建立的一个搜寻索引，就像在图书馆找书，假如一个图书馆没有索引，要找寻资料就会非常痛苦
- **.fseventsd** 是 File System Events Directory 的缩写，其实是一个档案夹，里面都是这个档案系统有做过的改变记录，它的重要性是在于使用 Spotlight 搜寻的时候，Spotlight 可以比较快知道哪些是新的档案或是哪些档案有被改变过，需要重新编档
- **.PKInstallSandboxManager** 
- **.PKInstallSandboxManager-SystemSoftware**
- **.DocumentRevisions-V100** 

### root/Library

Library 文件夹是比较复杂的文件夹，系统原装的资源库以及后来安装的应用软件的资源库都会在这里，但是又时候卸载只会删除 Application 文件中的程序，不会删除 Library 资源库中的相关文件。

- **Application Support** 应用相关的数据以及支持文件，比如第三方的插件、帮助应用、模板等；按照惯例，所有这些内容都会被存储在以应用名称命名的子目录当中
- **Assistants** 帮助用户进行配置或者其它任务的程序
- **Audio** 音频插件以及设备驱动
- **Caches** 用来选择色彩的资源，它们根据某种模型，比如 HLS (色彩角、饱和度、亮度) 选择器或者 RGB 选择器
- **Catacomb** 
- **ColorPickers**
- **ColorSync**  ColorSync 配置和脚本
- **Components** 系统包和扩展
- **Compositions**
- **Contextual Menu Items** 用于扩展系统级菜单的插件
- **CoreAnalytics** 
- **CoreMediaIO**
- **Desktop Pictures** 桌面图片目录
- **Developer**
- **DirectoryServices**
- **Documentation** 供计算机用户和管理员参考的文档文件和 Apple 帮助包
- **Extensions** 设备驱动和其它内核扩展（只存在于系统域中）
- **Filesystems** 
- **Fonts** 用于显示和打印的字体文件
- **Frameworks** 框架和共享库
- **GPUBundles**
- **Graphics**
- **Image Capture** 储存有多个 DC 厂商的标准驱动程序，当中还细分有两个档案夹，其中 Devices 中，苹果将各款不同DC细分成8个种类不同的驱动；此外，这裡还存放了各种和相机，Scanner 有关的驱动，例同 PTP（Picture Transfer Protocol），TWAIN 等
- **Input Methods** 安装的输入法
- **Internet Plug-Ins** 包含了 web 浏览器内容所需要的插件、库和过滤器
- **Java** Java运行环境
- **Keyboard Layouts** 键盘定义
- **Keychains** 钥匙串文件
- **LaunchAgents** 
- **LaunchDaemons** 
- **Logs** 控制台和系统服务的日志文件
- **MessageTracer**
- **Messages**
- **Modem Scripts** 调制解调器脚本
- **OpenDirectory**
- **PDF Services**
- **Perl** Perl 程序的功能扩展及库
- **PreferencePanes** 系统参数应用的插件
- **Preferences** 用户参数设置
- **Printers** 打印机驱动，PPD 插件和用来配置打印机的库
- **PrivilegedHelperTools** 
- **Python**
- **QuickLook** 快速查看插件
- **QuickTime** QuickTime 组件和扩展
- **Receipts** 安装过的 .pkg 安装包的替身，但不是.pkg安装包本身
- **Ruby**
- **Sandbox**
- **Screen Savers** 屏幕保护程序
- **ScriptingAdditions** 对 AppleScript 的功能进行扩展的脚本和脚本资源
- **Scripts** 各种程序所需要的脚本文件
- **Security**
- **Speech** 语音的相关资源文件
- **Spotlight**
- **StagedExtensions**
- **StartupItems** 在系统导入时刻运行的系统以及第三方脚本和程序
- **SystemMigration**
- **SystemProfiler**
- **Updates** 系统自动更新的安装文件，默认会自动删除里边的文件
- **User Pictures** 用户账号中，用户显示的图片的文件
- **Video**
- **WebServer**  web 服务器内容
- **Widgets** 已安装的Widget小工具

### user/files

- **Applications** 包含只有当前用户可以使用的程序，不过只是一个文件夹的名称而已，一般我会把一些数据库、GitHub 中的项目放到这里，自己的电脑自己用，因此诸如软件等等我还是直接放到 `/Applications`
- **Desktop** 显示在桌面上的所有文件
- **Documents** 个人用户的文档
- **Library** 包括应用程序设置及其它用户指定的系统资源或设置
- **Movies** QuickTime 或其它格式的影片
- **Music** 数字音乐文件，包括 iTunes 自动导入的音乐文件
- **Pictures** 图片文件夹
- **Public** 可以把需要与其它用户共享的文件放在这个目录中，默认状态下，这个目录可以被其它所有用户访问
- **Downloads** 下载文件夹

### user/.hidden_files

个人用户目录下的隐藏文件通常一些软件的用户的配置文件，装的应用越多，隐藏文件越多，这里列出了我的用户目录下几乎所有的隐藏文件，方便后期查询

- **.DS_Store** 是用来用户目录`~`文件夹的显示属性的：比如文件图标的摆放位置，删除以后的副作用就是这些信息的失去
- **.Trash** 垃圾桶
- **.bash_profile** profile 文件通常是用于设置系统的环境变量及启动程序，而`.bash_profile`是一个用户级的设置，只针对单个用户有效，因此每次登陆都会重新运行一遍这个文件
- **.bash_history** 命令历史，保存了 500 条在终端使用过的命令
- **.bash_sessions** 登陆终端的历史

由于我的操作，我的个人目录会出现一些不那么日常的隐藏文件，我把现有的隐藏文件列举在这里 : )

- **.ssh** 储存远程服务器连接密钥的文件夹，`id_rsa`是私钥，`id_rsa.pub`是公钥（密码算法通常有两种 dsa 和 rsa ），`known_host`记录了每个访问过的服务器的公钥
- **.vim** 文件夹中的`.netrwhist`文件是一个维护所有修改的目录的历史文件夹
- **.viminfo** 在 vim 中的操作行为会被 vim 自动记录下来，保存在`~/.viminfo`文件中，如：vim 打开文件时，光标会自动在上次离开的位置显示
- **.vimrc** 是 vim 的环境配置文件，整体的 vim 的设置是在`/etc/vimrc`文件中
- **.anaconda** 和 Anaconda Navigator 相关的配置
- **.bash_profile-anaconda3.bak**
- **.conda** 配置文件，包括个人用户的环境和个人的包
- **.condarc** conda 配置文件
- **.ipython** ipython 相关的配置文件
- **.kingsoft** 是和金山软件相关的用户配置文件夹
- **.config** 和金山软件相关的配置文件
- **.gitconfig** 和 git 相关的配置文件
- **.ShadowsocksX** 和 ShadowsockX 有关的用户配置文件夹
- **CFUserTextEncoding** 
- **.npm** npm 是有关 JavaScript 的包管理工具，是我在搭建博客的时候引入的隐藏文件，可直接删除，再次使用 npm 命令时将会重新引入`.npm`文件
- **.gem** 也是在搭建博客时引入的隐藏文件，可直接删除
- **.lesshst** 
- **.emacs.d**
- **.texpadtmp** Texpad 的临时文件

### user/Library

太累了就到这里吧！



「后记」博客主要参考了[详解MAC硬盘中各文件夹和Linux各文件夹](http://blog.sina.com.cn/s/blog_54cae6d70101dqnp.html)和 [Mac OS X Hidden Files & Directories](http://www.westwind.com/reference/OS-X/invisibles.html) ，后来觉得还是下载一个 CleanMyMac 来得方便，再次提醒自己莫要在细节上过分纠结。

