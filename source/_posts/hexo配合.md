title: "hexo配置 "
date: 2015-03-27 14:22:52
tags:
---
hexo系列教程：（四）hexo博客的优化技巧
上一节中我们已经学会了用hexo发布博客，这里再介绍一些小技巧对博客站点进行优化，实现更加丰富的功能。
后面的修改优化主要是针对 theme/light 的，如果你想偷懒直接使用配置好的主题，欢迎使用我的Lightum。如果你想使用其他主题，可以去Wiki挑选一款喜欢的。
添加“多说”评论
hexo默认使用国外比较流行的disqus，不过，按照“因地制宜”的原则，我们修改为国内用的多又好用的“多说”评论系统。步骤非常简单：
在多说进行注册，获得通用代码。
<!--more-->
将通用代码粘贴到themes\light\layout\_partial\comment.ejs里面，如下：
1
2
3
4
5
<% if ( page.comments){ %>
<section id="comment">
通用代码
</section>
<% } %>
很多网友反映自己使用的非 light 主题中找不到相应的文件。我的这些修改都是在 light主题中，其他主题请参考《Hexo使用多说教程》。
添加『页面导航』
在刚才添加「多说」评论的文件中，加入一段代码，如下：
1
2
3
4
5
6
7
8
9
10
11
12
13
<% if ( page.comments){ %>

 <nav id="pagination" >
    <% if (page.prev) { %>
    <a href="<%- config.root %><%- page.prev.path %>" class="alignleft prev" ><%= __('prev') %></a>
    <% } %>
    <% if (page.next) { %>
    <a href="<%- config.root %><%- page.next.path %>" class="alignright next" ><%= __('next') %></a>
    <% } %>
    <div class="clearfix"></div>
</nav>

<section id="comment">
添加“百度分享”
到百度分享获得代码，在themes/light/layout/_partial/article.ejs中，将<%-partial('post/share')%>删掉，替换为百度分享的代码。
添加小图标
在themes/light/layout/_partial/head.ejs里将<link href="<%- config.root %>favicon.png" rel="icon">替换为<link href="<%- config.root %>favicon.ico" rel="icon" type="image/x-ico">。将favicon.ico图标文件放在source目录下。制作图标的网站，http://www.faviconer.com。
添加分类、标签云widget
很简单，在themes/light/_config.yml中，添加如下：
1
2
3
widgets:
- category
- tagcloud
添加友情链接widget
在themes/light/layout/_widget中新建名为blogroll.ejs的文件，编辑内容如下：
1
2
3
4
5
6
<div class="widget tag">
<h3 class="title">友情链接</h3>
<ul class="entry">
<li><a href="http://zipperary.com/" title="Zippera's Blog">Zippera</a></li>
</ul>
</div>
在themes/light/_config.yml中，添加如下：
1
2
widgets:
- blogroll
生成post时默认生成categories配置项
在scaffolds/post.md中，添加一行categories:。同理可应用在page.md和photo.md。
添加新浪微博widget(微博秀)
去新浪微博开放平台设置和生成微博秀代码。
在themes/light/layout/_widget中新建名为weibo.ejs的文件，将刚才的代码直接保存到这里。
在themes/light/_config.yml中，添加如下：
1
2
widgets:
- weibo
导航栏添加”关于”
hexo new page "about"
到source/about/index.md编辑内容。
在themes/light/_config.yml中，添加如下：
1
2
menu:
  关于: /about
主页文章显示摘要
编辑md文件的时候，在要作为摘要的文字后面添加<!--more-->即可。
优化是无止境的，今天先写这些。
速度优化
由于 Google 被大陆屏蔽，Github 从大陆访问也比较慢，且不太稳定。所以一方面可以把 Blog 迁移到国内，比如我现在使用的Gitcafe提供的免费 Page 服务，又快又好用，赞一个，可以参考我写的《托管博客到gitcafe》 。另一方面，建议把 google 提供的 jquery 和 fonts api 全换掉。由于不同的主题其位置不同，最好是搜索一下。
Unix/Linux 用户在 shell 中切换到自己的主题目录下面；Windows 用户用 Git Bash 切换到主题目录下面。然后用grep 'jquery' -r ./搜索使用 jquery 的位置，如果是用的 google 的，则替换成国内的，我用的是百度，//libs.baidu.com/jquery/2.0.3/jquery.min.js， //libs.baidu.com/jquery/1.8.0/jquery.min.js，替换后如图（我的是 light 主题）：

然后替换google fonts，同样的方法，grep 'fonts' -r ./，找到后替换为//fonts.useso.com/css?family=Lato:400,400italic即可。
以上只是针对我的版本我的主题，读者根据自己的情况适当调整吧，比如 jquery 的版本号，你现在的是哪个版本就用 baidu 的哪个版本。把地址输入浏览器地址栏看能正确打开嘛，如果可以，说明是可用的。
全部替换完，更新自己的博客，然后查看源代码，看看是否全换成国内的了。