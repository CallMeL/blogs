---
title: "如何利用Hugo部署一个博客，比泡好杯面还快"
description: 
date: 2023-09-02T17:59:10+08:00
image: 
math: 
license: 
comments: true
draft: true
---

互联网上关于如何搭建部署Hugo网站的教程非常多，我自己踩过了一些坑之后把最快的部署步骤总结了出来。毕竟越快部署一个美观的网站就能越快开始做博客的真正目的--写作！  
最终搭建出来的网站效果类似于我现在的博客预览效果（时间截止至2023.09.02）。使用的主题是[hugo-theme-stack](https://github.com/CaiJimmy/hugo-theme-stack).  
PS. 我会尽量文字描述清楚，就不放截图了。

## 去超市买泡面：Github以及本地操作
首先需要取得我们博客的雏形，你需要一个可以访问<u>完全互联网<u>的电脑，以及一个github账户。  
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
### Hugo是什么以及怎么用
这个放到最后来说
### 修改模版的规则


## 可是我想加个蛋：先加上会更好的改善
### 让博客可被搜索

### 谷歌分析和页面访问统计
[Hugo的搭建与使用](http://www.amuro.top/other/hugo/)

## 参考链接
[“博客已运行x天x小时x分钟”字样](https://thirdshire.com/post/hugo-stack-renovation/#博客已运行x天x小时x分钟字样)
[总字数统计：“发表了x篇文章，共计x字”](https://thirdshire.com/post/hugo-stack-renovation/#总字数统计发表了x篇文章共计x字)
[Hugo_让你的博客被Google收录](https://huweim.github.io/post/blog_hugo_让你的博客被google收录/)
[Hugo的搭建与使用](http://www.amuro.top/other/hugo/)
[APLAYER FOR HUGO](https://tin6.com/post/install-aplayer-for-hugo/)
[Hugo对Markdown支持情况测试](https://edward852.github.io/post/markdown支持情况测试/)

{{< css.inline >}}
<style>
.greenbutton { background-color: green; color:white }
</style>
{{< /css.inline >}}