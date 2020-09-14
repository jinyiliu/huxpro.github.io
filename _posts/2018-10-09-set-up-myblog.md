---
layout:     post
title:      "欢乐搭博客"
subtitle:   "Hello world! Hello blog!"
date:       2018-10-9 12:00:00
author:     "Jinyi"
header-img: "img/home-bg-geek.jpg"
catalog: true
mathjax: true
tags:
    - 杂货铺
---

比较流行的静态博客框架有 [Hexo](https://hexo.io/zh-cn/) 和 [Jekyll](https://jekyllrb.com) ，Hexo的优点在于简化了搭建博客的操作，且有强大的插件系统，主题丰富；Jekyll 则是 GitHub Page 推荐的博客框架。我的博客是 fork 了 [HuxBlog](http://huangxuan.me) 之后改造的，如果不是因为 HuxBlog 的颜值是其它任何一个 Hexo 主题所无法比拟的，我会选择使用便捷的 Hexo 框架进行搭建。

希望博客搭建好之后可以方便自己整理知识，同时分享个人生活。



### Fork and Clone

在 Github 中`fork`的作用是拷贝原项目，并拥有修改权限。进入[Huxpro/huxpro.github.io](https://github.com/Huxpro/huxpro.github.io)，点击右上角的`fork`，可以得到自己的 jinyiliu/huxpro.github.io。然后进入 **Settings**，需要完成

- **Rename** 为 jinyiliu/jinyiliu.github.io
- **Custom domain** 为 jinyiliu.me（域名可以在 [GoDaddy](https://sg.godaddy.com/) 上使用支付宝购买），这一步实际上修改了`CNAME`文件，如果没有自己的域名，这一步也可以省略

接下来需要将这个 repo 克隆到本地，才能方便的进行测试和修改。由于 HuxBlog 本身包含了很多内容，从服务器克隆需要一段时间（在克隆前，需要设置 SSH Key）。



### 做一些修改

克隆到本地之后，可以打开自己的博客看一看 https://jinyiliu.github.io，是和 HuxBlog 完全一样的。如果想要使HuxBlog中显示自己的内容，只需要修改具体的文件即可，其中最重要的是对`_config.yml`文件的修改，下面做一些具体的修改说明。

- **Site settings** 需要修改
- **SNS settings** 是一些其他社交平台的账户信息，如果没有对应的用户名就使用`#`注释掉该行代码
- **Build settings** 是关于代码语法高亮的，不用修改
- **Gems** 提供了支持本地预览的功能，不用修改，但是克隆之后，可能需要按此提示安装`gem`和`jekyll-paginate`包
- **Disqus settings** [Disqus](https://disqus.com) 是一个评论系统，可以参考[这篇博客](https://www.jianshu.com/p/7e4453421b8f)注册用户、设置个人信息，不需要使用评论功能可以注释掉这些代码
- **Analytics settings** 是用来分析网页浏览数据等信息的，不需要可直接注释掉这些代码
- **Sidebar settings** 需要修改
- **Featured tags**、**Progressive Web Apps** 不用修改
- **MathJax** 是一个用来在网页中渲染公式的插件，因为我的博客将会需要大量的公式，最好将`page-mathjax`修改为`true`
- **Friends** 部分随自己开心

进入`img`文件夹，使用自己的图片和图标替换图片`avatar-hux-home.jpg`、`avatar-hux-ny.jpg`、`avatar-hux.jpg`、`favicon.icon`、`icon_wechat.png`等。修改替换文件`CNAME`、`index.html`、`README.md`、`_includes/about/zh.md`、`_includes/about/en.md`中的文本内容。现在这一些修改的要点在 Huxblog 的项目中已经有一些提示了。

隐藏或删除`_README.zh.md`、`_includes/posts`、`portfolio`，`about`。对`_posts`中的文件进行修改和替换。

HuxBlog 中的很多博文具有参考意义，如[饿了么的PWA升级](http://huangxuan.me/2017/07/12/upgrading-eleme-to-pwa/)提供了中英文的支持、[都 2015 年了，CSS 怎么还是这么糟糕](http://huangxuan.me/2015/12/28/css-sucks-2015/)中应用了幻灯片。下面是常见的一个 YAML 描述参数

```markdown
layout:		post
title:		"hello 2018"
subtitle:	"\"hello world, hello blog\""
date:		2018-10-10 12:00:00
author:		"Jinyi"
header-img:	"img/home-bg-art.jpg"
header-mask:	0.3
header-style:	text
lang:		en
catalog:	true
mathjax:	true
hidden:		true
multilingual:	true
tags:
    - 物理
    - 杂货铺
```

### Mathjax

这个博客模板是支持 Mathjax 的数学公式渲染的，需要在 YAML 中手动打开。但是又一些地方与 TyporaMD 的语法不太一样需要注意一下

- 最好使用 $\texttt{\begin{split}}$ 代替 $\texttt{\begin{align}}$ 否则对齐会出现问题
- 如需使用颜色用 $\texttt{\color{your_color}{your_text}}$

另外注意本地预览最好用 Chrome 预览，公式能够正常显示，用 Safari 预览的时候公式有时候不能正常显示。

