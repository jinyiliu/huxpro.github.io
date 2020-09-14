---
layout:		post
title:		"服务器编程相关配置"
subtitle:	"因为不想在自己电脑上装任何科学计算相关工具"
date:		2020-02-28 12:00:00
author:		"Jinyi"
header-img:	"img/in-post/2020-02-28-ubuntu-vim.assets/bg.png"
header-mask:	0.4
lang:		en
catalog:	true
mathjax:	true
tags:
    - Linux
---

感谢 [PegasusWang](https://space.bilibili.com/288339968/) 的 Vim 课程让我认识到了 Vim 的强大，这篇博客将记录一些服务器 Vim 编程的一些常用配置，这里仅仅提供一侧参考，后来因为种种原因我不再使用 Vim 投向了 VScode 的怀抱，真香！

### Zsh

我选择 Zsh 来作为我的 shell ，其实主要是因为如果你习惯使用 Bash 的话，可以无缝迁移到 Zsh 并且还能发现 Zsh 的很多优于 Bash 的人性化配置。可以使用`cat /etc/shells`来查看当前所有可以使用的 Shell ，如果没有 Zsh 可以使用如下两行命令安装并修改自己的 Shell

```bash
sudo apt-get install zsh
chsh -s /bin/zsh
```

这时所有的配置文件都在 .zshrc 中了。随后安装 Zsh 的标配 [Oh my Zsh](https://ohmyz.sh) 并且可以设置 Zsh 的主题等让使用体验更好。我认为默认的主题就很简洁而优秀了，所以这里就没有特别配置。

```bash
sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

### Vim

首先是 Vim 的安装，为了后期更好的配置 Vim 需要，使用至少 Vim8 的版本（支持异步），可以通过`vim --version`来查看 Vim 的版本。如果有超级用户的权限首先更新源`sudo apt-get update `然后安装`sudo apt install vim`即可。如果没有超级用户的权限，可以根据 [GitHub](https://github.com/vim/vim) 上的指示下载进行安装。学习 Vim 的使用操作可以参考 PegasusWang 的[慕课课程](https://www.imooc.com/learn/1129)，非常全面，一些概念比如 Vim 中的 buffer 等也解释得非常清楚。

Vim 的灵魂就在于其所有操作都不依赖鼠标，这是它高效的原因也是它难以学习、对于初学者不太友好的原因，但只要努力记住这些快捷键，形成肌肉记忆，编写代码依靠的就是脊神经反射，快得飞起！

<img src="/img/in-post/2020-02-28-ubuntu-vim.assets/vim.png">

Vim 的快捷键很多，但只要记住其中一小部分就足够日常的编程操作了，当然为了方便自己使用，通常会在 .vimrc 中修改键位的映射。

如果要最大程度地发挥 Vim 的作用，还是需要依赖各种各样的插件，不同插件也会有不同的键位映射。插件可以通过插件管理器 [vim-plug](https://github.com/junegunn/vim-plug) 进行安装。我日常的插件配置可以参见 [myrc/.vimrc](https://github.com/jinyiliu/myrc/blob/master/.vimrc) 文件，但是因为我后期依靠 VScode 为主要的编辑器，服务器上 Vim 的插件其实就不需要特别复杂。

有一些插件可能比较难以安装，比如 [tagbar](https://github.com/majutsushi/tagbar) 这个插件，它依赖 [Universal Ctags](https://ctags.io/) ，而 Ctags 可以简单按照官方的 [doc](https://docs.ctags.io/en/latest/autotools.html#gnu-linux-distributions) 来实现安装，Ctags 本身有很多依赖，首先需要要安装

```bash
sudo apt install gcc make \
    pkg-config autoconf automake \
    python3-docutils \
    libseccomp-dev \
    libjansson-dev \
    libyaml-dev \
    libxml2-dev
```

随后克隆 [Universal Ctags](https://ctags.io/) 到本地，进入 Ctags 的目录并依次执行

```bash
./autogen.sh
./configure --prefix=/where/you/want
make
make install
```

以上这一切都是在有超级用户权限的情况下完成的。如果没有超级用户的权限，那么将会更加复杂。

### Tmux

Tmux（Terminal multiplexer）终端复用器相当于原来 Linux 中的终端屏幕管理器 Screen 升级版。Tmux 的作用相当于在终端中创造了一个工作空间，即使退出服务器也可以依然继续运行程序，下一次登入服务器时再次打开这个工作空间即可，Tmux 中的 session 、window 和 pane 的概念如下

<img src="/img/in-post/2020-02-28-ubuntu-vim.assets/tmux.jpg">

### iTerm

终端使用 iTerm2 来代替 Mac 自带的终端，因为 iTerm2 又一些功能解决了痛点。比如在 iTerm 中使用 [imgcat](https://github.com/eddieantonio/imgcat) 可以直接利用这个命令在终端中渲染图片。另外一个很特别的功能就是 iTerm 和 Tmux 的集成，不用再死记 Tmux 的快捷键了

```bash
tmux -CC
tmux -CC attach
tmux -CC attach -t session_name
tmux -CC new -s new_session_name
tmux kill-session -t session_name
```

### Jupyter Notebook

还有一个和服务器交互的方式就是利用 Jupyter Notebook 可以参考[这个知乎链接](https://zhuanlan.zhihu.com/p/69869583)，关于 SSL 自签证书参考这个[博客](https://www.cnblogs.com/lihuang/articles/4205540.html)。

```bash
$ openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout mykey.key -out mycert.pem
```

Jupyter Notebook 在远程连接的过程中，可能会出现无法连接到 kernel 的问题，这有可能是因为 Jupyter Notebook 的版本和其依赖 tornado 的版本不匹配，升级 Jupyter Notebook 或降级 tornado 就行了。

### 修改 Mac 键位映射

将`Ctrl`与`Caps Lock`互换键位。具体操作是打开偏好设置，进入键盘，最后进入修饰键修改相应的键位即可。在 Vim 的操作中`Ctrl`是更为常见的快捷键前缀，互换这两个键位有利于手指操作。

### 开启 FTP 服务

需要在服务器上开启 FTP 服务（SFTP 协议）才能更好地与 Mac 交互进行文件传输，首先`sudo apt install vsftpd`安装包，然后编辑`sudo vi /etc/vsftpd.user_allowlist`把自己的用户名输进去，最后`sudo vi /etc/vsftpd.conf`修改配置文件

```vim
write_enable=YES
userlist_file=/etc/vsftpd.user_allowlist
userlist_enable=YES
userlist_deny=NO
```

上面被注释掉的行取消注释，没有的行添加进去，最后在终端输入`sudo service vsftpd restart`重启 FTP 服务即可。而在 Mac 端，打开访达，快捷键`Cmd + K`前往连接服务器

<img src="/img/in-post/2020-02-28-ubuntu-vim.assets/ftp.png" width="80%">

输入服务器地址，就可以在访达里浏览服务器中的文件并自由下载了。但是如果需要上传、修改服务器里的文件等更复杂的操作还需要其它的 FTP 应用。但是从 VScode 上直接下载数据也太香了。

