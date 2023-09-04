---
title: "如何利用Hugo部署一个博客，比泡好杯面还快"
description: 
date: 2023-09-02T17:59:10+08:00
image: 
math: 
license: 
comments: true
draft: false
categories:
    - 装修记录
tags: ['Hugo']
---

互联网上关于如何搭建部署Hugo网站的教程非常多，我自己踩过了一些坑之后把最快的部署步骤总结了出来。毕竟越快部署一个美观的网站就能越快开始做博客的真正目的--写作！  
最终搭建出来的网站效果类似于我现在的博客预览效果（时间截止至2023.09.02）。使用的主题是[hugo-theme-stack](https://github.com/CaiJimmy/hugo-theme-stack).  其他主题可以到[Hugo Themes](https://themes.gohugo.io)中挑选下载，不过不一定适用本文的【】章节。可以直接谷歌搜索`主题名+Hugo教程`自行参考搭建。
PS. ~~因为懒~~ 我会尽量文字描述清楚，就不放截图了。

## 去超市买泡面：Github以及本地操作
首先需要取得我们博客的雏形，你需要一个可以访问<u>完全互联网<u>的电脑，以及一个github账户。  
0. 在电脑上安装hugo：`brew install hugo`
1. 打开[hugo-theme-stack-starter](https://github.com/CaiJimmy/hugo-theme-stack-starter)。选择绿色的<p class="greenbutton">Use this template</p>按钮，跳转到新页面之后自定义项目名称，选择保存。  
2. 在自己的这个项目里复制项目的https或者ssh链接，用`git clone`命令克隆到本地。  
3. 在下载的文件夹根目录下打开终端/命令行，输入`hugo server`开始运行网站。在浏览器输入[http://127.0.0.1:1313](http://127.0.0.1:1313)就可以浏览示例网站，和[主题demo网站](demo.stack.jimmycai.com)应该是一模一样的。

至此如果没有任何报错，那么恭喜你，再点几下鼠标你的博客就可以发布了。


## 烧开水：Vercel

1. 注册一个[vercel](https://vercel.com/dashboard)账号，我们要给自己的博客一个别人可以访问的链接。建议直接用github账号注册，这样之后可以直接拉取到自己的仓库。  
2. 在主页点击Add New按钮，选择Project
3. 选择刚刚通过模版保存的仓库，点击import  
4. Build & Development Settings这一个空一定上拉选择Hugo模版  
5. Build Command填写`amazon-linux-extras install golang1.11 && hugo --gc --minify` (需要把override勾选上);Output Directory 填写 `public`
6. 在Environment Variables中新增一个名称为`HUGO_VERSION`，值为`0.93.2`的变量
7. 点击deploy，稍等一下就会得到一个以.vercel.app结尾的网页，这个就是博客目前的链接啦！

## 用漂亮的碗装泡面：添加自己的域名
根据小球飞鱼这篇[Hugo | 为 Blog 添加自定义域名](https://mantyke.icu/posts/2021/7e64c334/)里的推荐，我在[Dynadot](https://www.dynadot.com)购买了自己的域名。
选择好心仪的域名购买好后就可以在vercel上修改博客的链接了。
1. 在Dynadot的My Domain页面配置DNS：假设你购买的域名是abc.com。
你想让abc.com作为你博客的访问链接，就在Domain Record中新增record，然后选择Record Type为`CNAME`，IP Address or Target Host输入`cname.vercel-dns.com`。
如果你想让subdomain.abc.com作为你博客的访问链接（比如blog.abc.com），就在下方的Subdomain Records 中新增record，subdomain填写`blog`,然后选择Record Type为`CNAME`，IP Address or Target Host输入`cname.vercel-dns.com`。
2. 在Vercel主页中点开刚刚发布的网站，找到最右边的setting页面，点击后选择左侧菜单的Domain，添加abc.com或者subdomain.abc.com，验证之后就可以生效。

如果不想自己购买域名，也嫌弃vercel提供的域名，可以参考[Hugo | 一起动手搭建个人博客吧](https://mantyke.icu/posts/2021/hugo-build-blog/)最后的Q&A用github托管网站。

## 拿起叉子吧：最基本的使用规则

好了一切已经准备就绪！首先让我们在博客的根目录运行`hugo serve`，到[http://127.0.0.1:1313](http://127.0.0.1:1313)可以到处点点看看！
~~等泡面泡好的时间里，~~ 我们可以来先看一下一直在说的Hugo到底是什么。根据[官方的文档](https://gohugo.io/documentation/)：<u>Hugo is the world’s fastest static website engine. It’s written in Go (aka Golang).<u> 

Static website engine 静态网站引擎，就是通过模版选择和自己的配置，生成静态网页的工具。
我们利用这个引擎，不用从零开始一个一个去写CSS和HTML文件，而是直接用别人配置好页面去填充东西。
相当于比起自己从买菜切菜杆面来做一碗面，我们直接从从超市里选了别人调配好的方便面，只需要根据自己的喜好去加减调料。
网络上有许多教程，推荐先去阅读[Hugo 从入门到会用](https://olowolo.com/post/hugo-quick-start/#%E5%BC%80%E5%A7%8B%E5%86%99%E4%BD%9C)，以了解基本的文件组织结构。


* 站名等修改
    为了让这个博客看上去是你自己的，需要去：  
    到 `config/_default/config.toml`文件中修改站名，将默认语言换成中文（languageCode和defaultContentLanguage赋值为`zh-cn`。  
    到  `config/_default/params.toml`中修改favicon，footer，sidebar等信息。

* 新建和编辑文章

    最重要的一个文件夹是`content/post`文件夹，这里存放了我们要发的内容。每个文章对应一个文件夹，文章的内容书写在该文件夹下的`index.md`文件中。如果要新建一个文章，我们也需要在post文件夹下新建一个任意名称的文件夹，和index.md文件（有的主题是不需要用`index`去命名文件，但是stack这个主题是需要的）
    每个index.md文件有两个部分组成：
    1. 两个`---`之间的是该文章的页面参数，包括标题，发表日期等等。完整的参数列表可以看[Front Matter](https://olowolo.com/post/hugo-quick-start/#front-matter)。
    2. 正文部分，完全按照markdown的语法规则书写，最终渲染结果根据选择的主题不同的不同。如果不熟悉markdown语法的，可以参考[Hugo对Markdown支持情况测试](https://edward852.github.io/post/markdown支持情况测试/)。可以在hello-world文件夹下的index.md尝试着做一下修改，比如title，tags等（输入`hugo serve`后博客会一直在本地运行，每次修改的保存都会实时更新在[http://127.0.0.1:1313](http://127.0.0.1:1313) ）


* 新建分类和标签

    categories和tags这两个标签在每篇文章的参数部分加了新的之后，主页的分类会自动更新。如果想实现点进这个分类的页面的话，需要在content的catergories或者tags文件夹下添加对应的文件夹，该文件夹下要有一个`_index.md `文件。比如我希望`Hugo`
    这个标签有一个单独的标签页，就一定要有`content/tags/Hugo/_index.md`这个文件，标签的封面图放在`Hugo`文件夹下即可


## 可是我想加个蛋：先加上会更好的改善
### 修改模版的规则
我这里先假设目前你的文件结构和内容和[hugo-theme-stack-starter](https://github.com/CaiJimmy/hugo-theme-stack-starter)模版中的是一模一样。因为是从模版搭建，所以目前我们还没有现成可以去修改的文档。我们需要新建正确的文件夹和正确的文件名才能修改到想修改的地方，比如页脚。我的做法是：
    1. 切换到当前博客的根目录下输入`git submodule add https://github.com/whuwangyong/hugo-theme-stack/ themes/hugo-theme-stack`，下载完后会出现一个`/themes/hugo-theme-stack`文件夹
    2. 拷贝`/themes/hugo-theme-stack/layouts`和`/themes/hugo-theme-stack/assets`到博客根目录下（有重复直接替换就好）
这下我们就在layouts和assets进行模版的修改。layout中其实就是按照文章页每个部分的来命名文件夹以及做设置。比如页脚叫footer，侧边栏叫sidebar，在对应的html文件修改自己想要的即可。更详细的可以阅读[如何自訂Hugo主題：程式碼覆寫](https://ivonblog.com/posts/customize-and-override-hugo-themes/)

### 页脚添加运行时间，访问人次和发表文字数
我是按照第三夏尔的[“博客已运行x天x小时x分钟”字样](https://thirdshire.com/post/hugo-stack-renovation/#博客已运行x天x小时x分钟字样)和[总字数统计：“发表了x篇文章，共计x字”](https://thirdshire.com/post/hugo-stack-renovation/#总字数统计发表了x篇文章共计x字)来给页脚添加运行时间和发表文章数。


### 谷歌分析和页面访问统计
参考Amuro Peng的[Hugo的搭建与使用](http://www.amuro.top/other/hugo/)，开通[谷歌分析](https://marketingplatform.google.com/about/analytics/)，并在其中新增一个账号和应用，获取该应用的追踪ID。
1. 在`confid/_defult/config.toml`中添加`googleAnalytics = "G-XXXXX（你的追踪ID）"`
2. 在`\layouts\partials\header.html`添加以下代码
    ```
    <!-- 添加谷歌分析插件Google Analytics -->
    {{ template "_internal/google_analytics.html" . }}
    ```

### 添加评论 
参考[Waline快速上手](https://waline.js.org/guide/get-started/#leancloud-设置-数据库)配置好LeanCloud和Vercel后，在`confid/_defult/params.toml`中添加
```
[comments]
enabled = true
provider = "waline"


[comments.waline]
serverURL = "https://blog-comments-murc60bpk-callmel.vercel.app"
lang = "zh-CN"
visitor = true
avatar = ""
emoji = ["https://cdn.jsdelivr.net/gh/walinejs/emojis/weibo"]
requiredMeta = ["name", "email"]
placeholder = ""
DISABLE_REGION = true
DISABLE_USERAGENT = true

[comments.waline.locale]
admin = "潮潮"
```
### 可搜索
完全参考[让Google搜索到自己的博客](https://zoharandroid.github.io/2019-08-03-让谷歌搜索到自己的博客/)

### 相册
## 参考链接
[“博客已运行x天x小时x分钟”字样](https://thirdshire.com/post/hugo-stack-renovation/#博客已运行x天x小时x分钟字样)

[Hugo_让你的博客被Google收录](https://huweim.github.io/post/blog_hugo_让你的博客被google收录/)
[Hugo的搭建与使用](http://www.amuro.top/other/hugo/)
[APLAYER FOR HUGO](https://tin6.com/post/install-aplayer-for-hugo/)
[Hugo对Markdown支持情况测试](https://edward852.github.io/post/markdown支持情况测试/)

{{< css.inline >}}
<style>
.greenbutton { background-color: green; color:white }
</style>
{{< /css.inline >}}