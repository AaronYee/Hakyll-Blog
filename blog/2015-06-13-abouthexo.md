---
title: 关于 Hexo ，也就是那些事儿
tags: hexo,技术杂谈
---


<!--more-->

![](/assets/images/abouthexo/hexo.png)

### 前言
---
这篇博文主要介绍用hexo写blog中所涉及到的一些内容，内容参考自[hexo官方文档](http://hexo.io/zh-cn/docs/)和[ijiaober的Hexo使用攻略系列](http://ijiaober.github.io/categories/hexo/)。

### Hexo简介
---
* **Q. 什么是Hexo？**
  > 快速、简洁且高效的博客框架，made by [Tommy Chen](http://tommy-chen.com/)。(Tommy Chen的个人主页太炫酷了。)

* **Q. Hexo的优势？**
> * 超快速度，Node.js 所带来的超快生成速度，让上百个页面在几秒内瞬间完成渲染。
  * 支持Markdown，Hexo 支持 GitHub Flavored Markdown 的所有功能，甚至可以整合 Octopress 的大多数插件。
  * 一键部署，只需一条指令即可部署到 GitHub Pages, Heroku 或其他网站。
  * 丰富的插件，Hexo 拥有强大的插件系统，安装插件可以让 Hexo 支持 Jade, CoffeeScript。
  * 简单的操作，几条命令即可完成blog框架的搭建。
    	$ npm install hexo-cli -g
 	   $ hexo init blog
		$ cd blog
		$ npm install
		$ hexo server

### Hexo安装
---
安装Hexo很简单，需要在安装前确认已经安装下列应用程序：
* [Node.js](https://nodejs.org/)
* [Git](http://git-scm.com/)
接下来只需要在Git bash中使用npm即可完成Hexo的安装。
		$ npm install -g hexo-cli
若Git bash中提示 **npm command not found**，请检查 **Node.js** 的配置信息，是否将 **Node.js** 的路径加入到环境变量中（建议安装 **Node.js** 时不要修改默认安装路径）。若确认无误仍出现上述错误，请打开 **windows command** 命令行，进入 **node.js** 安装路径下尝试安装。					
		C:\Program Files\nodejs\node_modules\npm> npm install -g hexo-cli
测试，若输入命令后出现类似下述内容后，则证明安装成功。
		$ hexo version
		hexo: 3.1.1
		os: Windows_NT
		http_parser: 2.3
		node: 0.12.4
		v8: 3.28.71.19

### Hexo初探
---
Hexo安装成功后，我们首先来试用一下。首先创建一个我们想要保存blog信息的文件夹，anyway，anywhere。然后，打开 git bash，执行以下命令。

    $ hexo init <folder>
    $ cd <folder>
    $ npm install
其中的 **&lt;folder>** 为我们刚刚所建立的文件夹名称，注意存放位置的问题，此处需使用**文件夹的绝对路径**。也可以先用 git bash 进入到目录文件夹，再执行初始化操作。观察我们刚刚所建立的文件夹，会发现其中多出了如下的文件。


	.
	├── node_modules
	├── _config.yml        
	├── package.json       
	├── scaffolds          
	├── scripts            
	├── source             
	|   ├── _drafts
	|   └── _posts
	└── themes       

关于各个文件夹，我们稍后再详细介绍。接下来，我们使用 Hexo 预带的内容生成第一个静态页面。

	$ hexo generate    // hexo g is also okay    

观察 blog 文件夹下，会发现多出了 public 文件夹，这便是我们所产生的静态网页文件所存放的位置。

然后开启 local 本地端hexo服务器。

	$ npm install hexo-server --save
	$ hexo server     // hexo s is also okay

打开浏览器，地址栏输入 `http://localhost:4000` 即可观察到hexo预带的网页展示。

关于如何本地的网页部署到Github端，请参考[Github page 搭配 Hexo 搭建独立博客](http://aaronyee.github.io/2015/06/12/hello-world/)。

### Hexo管理与配置
---
谈到 Hexo 的管理，我们首先来看一下 blog 根目录下每个文件夹的作用。

* `node_modules`，这个文件夹中存放的主要是 hexo 的相关插件，我们通过命令 `npm install` 所安装的插件包便存放在这个文件夹中，除了默认安装的插件外，如缺少插件可采用如下命令的格式来安装。

		$ npm install hexo-generator-index --save
		$ npm install hexo-generator-archive --save
		$ npm install hexo-generator-category --save
		$ npm install hexo-generator-tag --save
		$ npm install hexo-server --save
		$ npm install hexo-deployer-git --save
		$ npm install hexo-deployer-heroku --save
		$ npm install hexo-deployer-rsync --save
		$ npm install hexo-deployer-openshift --save
		$ npm install hexo-renderer-marked@0.2 --save
		$ npm install hexo-renderer-stylus@0.2 --save
		$ npm install hexo-generator-feed@1 --save
		$ npm install hexo-generator-sitemap@1 --save

* `public`，这个文件夹中存放的是我们使用hexo框架+Markdown语法写出的blog经过动态编译后形成的静态网页文件，包括 css 与 js 的内容。若想将本地的 blog 部署到服务器端（如 Github page ），只需将`public`文件夹中的内容上传到服务器端即可。

* `scaffolds`，这个文件夹中存放的是创建新的 blog 时的模板信息，所以如果有固定的写作样式等等，可以通过配置这个文件夹中的相应文件达到目的。

		title: { title }
 	   date: { date }
		categories:
		tags:
		---
 如我的`scaffolds/post.md`中的内容如下所示，那么每次我`hexo new {title}`写新的 blog 的时候，上述内容便会自动出现在新的 blog 的开头。

* `source`，这个文件夹中是我们本地的资源文件夹，例如我们通过`hexo new {title}`生成的 blog 便会存在于 `source/_posts`文件夹中。

* `themes`，这个文件夹中存放的是我们搭配 blog 框架时候所使用的主题信息，`hexo 3.1.1`的默认主题是 `landscape`。

* `_config.yml`，这个文件是我们整个 blog 框架的配置信息。下面贴出个人的配置文件并附上注释信息，大家可根据自己的需要进行修改。
		# Hexo Configuration
		## Docs: http://hexo.io/docs/configuration.html
		## Source: https://github.com/hexojs/hexo/

		# Site
		title: Aaron-Yee Blog                       # // 网站标题
		subtitle: 专注 & 沉淀                       # // 网站副标题
		description:                                # // 网站描述
		author: Aaron Yee                           # // 作者名字
		language: zh-CN                             # // 网站使用的语言
		timezone:

		# URL
		## If your site is put in a subdirectory, set url as 'http://yoursite.com/child' and root as '/child/'
		url: http://yoursite.com
		root: /
		about_dir: about
		tag_dir: tags
		category_dir: categories
		permalink: :year/:month/:day/:title/
		permalink_defaults:

		# Directory                                 // 目录
		source_dir: source                          # // 资源文件夹，用来存放内容
		public_dir: public                          # // 公共文件夹，用于存放生成的站点文件
		tag_dir: tags                               # // 标签文件夹
		archive_dir: archives                       # // 归档文件夹
		category_dir: categories                    # // 分类文件夹
		code_dir: downloads/code                    # // include code 文件夹
		i18n_dir: :lang                             # // 国际化(i18n)文件夹
		skip_render:                                # // 跳过指定文件的渲染

		# Writing                                   // 设置hexo new 时候的相关配置
		new_post_name: :title.md                    # // 新文章文件名称 # File name of new posts                
		default_layout: post                        # // 预设布局
		titlecase: false                            # // 把标题转换为title case # Transform title into titlecase
		external_link: true                         # // 在新标签中打开链接 # Open external links in new tab
		filename_case: 0                            # // 把文件名称转换为(1)小写或(2)大写
		render_drafts: false                        # // 显示草稿
		post_asset_folder: false                    # // 启动Asset文件夹
		relative_link: false                        # // 把链接改为与根目录的相对位置
		future: true                                # // 显示未来的文章
		highlight:                                  # // 代码块设置
		  enable: true
		  line_number: true
		  auto_detect: true
		  tab_replace:

		# Category & Tag                            // 分类 & 标签
		default_category: uncategorized
		category_map:
		        机器学习: Machine Learning
		        深度学习: Deep Learning
		        技术杂谈: tittle-tattle
		tag_map:

		# Date / Time format
		## Hexo uses Moment.js to parse and display date
		## You can customize the date format as defined in
		## http://momentjs.com/docs/#/displaying/format/
		date_format: YYYY-MM-DD
		time_format: HH:mm:ss

		# Pagination
		## Set per_page to 0 to disable pagination
		per_page: 10
		pagination_dir: page

		# Extensions
		## Plugins: http://hexo.io/plugins/
		## Themes: http://hexo.io/themes/
		theme: jacman                              # // 主题名称

		# Deployment
		## Docs: http://hexo.io/docs/deployment.html
		deploy:
		  type: git
		  repo: https://github.com/AaronYee/AaronYee.github.io.git
		  branch: master

关于上述配置信息如果还有不明白的地方，请参考[Hexo 的官方文档](http://hexo.io/zh-cn/docs/configuration.html)。

### Hexo命令
---
Hexo 的命令都是在类似于 Git bash 这样的终端中来输入的。

*	新建一个网站框架（即整个 blog）。如果没有设置 folder ，Hexo 默认是在当前的工作目录下建立网站框架。		
			$ hexo init [folder]
*	新建一篇 blog 。如果没有设置 layout 的话，默认使用 **_config.yml** 中的 **default_layout** 参数代替。如果标题包含空格的话，请使用引号括起来。(`< >` 符号不必打出。)
		
			$ hexo new [layout] < title >

*	生成静态文件。

			$ hexo generate 
			$ hexo generate --deploy       // 表示文件生成后立即部署到服务器端.
			$ hexo generate --watch        // 监视文件变动并立即重新生成静态文件，在生成时会比对文件的 SHA1 checksum，只有变动的文件才会写入。

*   发表草稿。

			$ hexo publish [layout] < filename >
*	启动本地端服务器。
			$ hexo server
			$ hexo server -p 5000          // 将端口更改为5000
			$ hexo server -s               // 静态模式服务器只处理 public 文件夹内的文件，而不会处理文件变动，执行时应该先自行执行 hexo generate。
			$ hexo server -i 192.168.1.1   // 服务器默认运行在 `0.0.0.0`，可以覆盖默认的 IP 设置。
*   部署网站，只需一条命令就能将网站部署到服务器上。
			$ hexo deploy
	但在开始之前，需要安装`hexo-deployer-git`插件。
			$ npm install hexo-deployer-git --save
	修改`_config.yml`的参数设置。以部署到 Github page 为例，用文本编辑器打开`_config.yml`，找到 deploy 选项，修改参数。
			# Deployment
			## Docs: http://hexo.io/docs/deployment.html
			deploy:
			  type: git
			  repo: < repository url >     // repository url 替换为个人的Github page地址
			  branch: master 			   // 分支名称。如果您使用的是 GitHub 或 GitCafe 的话，程序会尝试自动检测。

	部署到其他地方的话，请参考[官方文档](http://hexo.io/zh-cn/docs/deployment.html)。
*	从其他系统迁移到Hexo。具体内容请参考[hexo迁移](http://hexo.io/zh-cn/docs/migration.html)。
			$ hexo migrate < type >

更多命令请参考[hexo官方文档——命令](http://hexo.io/zh-cn/docs/commands.html)。

那么，我们使用 Hexo 写博文的整个流程大概是这样的。
			
			$ mkdir "blog folder"
			$ cd "blog folder"
			$ hexo init
			$ npm install
			$ hexo new "blog title"
			$ echo " " > "blog title"      // 双引号中的内容表示 blog的内容，此处推荐使用文本编辑器编辑 hexo new 命令生成的 "blog title".md 文件。
			$ hexo generate
			$ hexo server                  // 在本地服务器端调试，待确认无误后，上传到Github page服务器。
			$ hexo deploy


### 玩转Hexo
---
此处我假设我们都已经按照上文搭建好了我们的框架，但是打开主页我们会发现很多地方我们不满意，那么应该怎么修改呢？实际上，**每个主题有各自不同的修改方法**，此处以 Hexo 自带的 landscape 主题为例。没错，这些东东都是由这个叫做**主题**的东东引起的。

那么应该怎么修改特定主题的内容呢？答案就在`./themes/landscape/_config.yml`这个文件中。

* **导航栏**。打开主页我们会发现 landscape 这个主题只有`Home`和`Archives`两项，那么怎么添加呢？文本编辑器打开`./themes/landscape/_config.yml`文件，在最上方我们可以看到。

		# Header
		menu:
		  Home: /
		  Archives: /archives
		rss: /atom.xml
  Okay，我们只需要把想加入导航栏的内容按照上面的格式添加进去即可，例如，我们想添加 About 项。
  		# Header
		menu:
		  Home: /
		  Archives: /archives
		  About: /about
		rss: /atom.xml
  注意，**配置文件中的`;`后必须有一个空格！**`;`后的内容表示访问路径，接下来我们只需要在 `blog/source`目录下增加一个`about`文件夹，并在其中添加一个`index.md`文件，当我们在主页点击 About 后，页面便会跳转到我们刚刚所编辑的这个`index.md`所生成的静态网页中，`index.md`的内容可按照个人需求来写。

* **评论和分享**。怎么添加 blog 的评论和分享功能呢？blog 中的评论系统国内一般采用“多说”，国外用“Disqus”较多，可根据自己的需求进行配置，以多说为例。**实际上，每个不同的主题有不同的配置方法！**这里，我们只是以 Hexo 预带的 landscape 主题为例。

  访问[多说](http://duoshuo.com/)，使用其中一种途径登陆后会有设置**域名**，**名称**和**首页网址**，首页网址填写为我们的**Github page 地址**，如(username.github.io)。 **名称为我们 Github 的 username **。
  然后，使用文本编辑器打开`/themes/landscape/layout/_partial/article.ejs`文件，把
		
		<% if (!index && post.comments && config.disqus_shortname){ %>
		  <section id="comments">
		    <div id="disqus_thread">
		      <noscript>Please enable JavaScript to view the <a href="//disqus.com/?ref_noscript">comments powered by Disqus.</a></noscript>
		    </div>
		  </section>
		<% } %>
   
   改为

		<% if (!index && post.comments && config.duoshuo_shortname){ %>
	    <section id="comments">
	    	<!-- 多说评论框 start -->
	    	<div class="ds-thread" data-thread-key="<%= post.layout %>-<%= post.slug %>" data-title="<%= post.title %>" data-url="<%= page.permalink %>"></div>
	    	<!-- 多说评论框 end -->
	    	<!-- 多说公共JS代码 start (一个网页只需插入一次) -->
	    <script type="text/javascript">
	    var duoshuoQuery = {short_name:'<%= config.duoshuo_shortname %>'};
	      (function() {
	        var ds = document.createElement('script');
	        ds.type = 'text/javascript';ds.async = true;
	        ds.src = (document.location.protocol == 'https:' ? 'https:' : 'http:') + '//static.duoshuo.com/embed.js';
	        ds.charset = 'UTF-8';
	        (document.getElementsByTagName('head')[0] 
	         || document.getElementsByTagName('body')[0]).appendChild(ds);
	      })();
	      </script>
	    <!-- 多说公共JS代码 end -->
	  </section>
	  <% } %>

  然后打开根目录的配置文件`./_config.yml`，在其中加入以下代码。

  		duoshuo_shortname: username                  // 这里的username请用 Github 的 username 替换。

  分享，**landscape** 主题已经自带了分享功能，但分享的对象都是 **Facebook，Twitter** 等国内不常见的网站，那么应该怎样添加或修改呢？

  首先，打开`./themes/landscape/source/js/script.js`文件，在其中找到如下代码：

		  var html = [
		    '<div id="' + id + '" class="article-share-box">',
		        '<input class="article-share-input" value="' + url + '">',
		        '<div class="article-share-links">',
		           '<a href="https://twitter.com/intent/tweet?url=' + encodedUrl + '" class="article-share-twitter" target="_blank" title="Twitter"></a>',
		           '<a href="https://www.facebook.com/sharer.php?u=' + encodedUrl + '" class="article-share-facebook" target="_blank" title="Facebook"></a>',
		           '<a href="http://pinterest.com/pin/create/button/?url=' + encodedUrl + '" class="article-share-pinterest" target="_blank" title="Pinterest"></a>',
		           '<a href="https://plus.google.com/share?url=' + encodedUrl + '" class="article-share-google" target="_blank" title="Google+"></a>',
		        '</div>',
		    '</div>'
		  ].join('');

 可以看到其中形如`<a href="https://twitter.com/intent/tweet?url=' + encodedUrl + '" class="article-share-twitter" target="_blank" title="Twitter"></a>`的即为分享地址，那么我们可以加入国内常用的一些社交工具，如下所示
		 '<a href="http://service.weibo.com/share/share.php?&title=' + encodedUrl + '" class="article-share-sina" target="_blank" title="微博"></a>',
		'<a href="http://share.renren.com/share/buttonshare.do?link=' + encodedUrl + '" class="article-share-renren" target="_blank" title="人人"></a>',
		'<a href="http://sns.qzone.qq.com/cgi-bin/qzshare/cgi_qzshare_onekey?url=' + encodedUrl + '" class="article-share-qq" target="_blank" title="QQ 空间"></a>',
		'<a href="http://v.t.qq.com/share/share.php?url=' + encodedUrl + '" class="article-share-tencent" target="_blank" title="腾讯微博"></a>',

加入代码之后，我们需要加入网站的图标。本主题使用 Font Awesome 来显示图标，但内置的 Font Awesome 版本较旧，无法显示 QQ、腾讯微博等图标，所以，需要下载[最新版 Font Awesome](http://fortawesome.github.io/Font-Awesome/)，替换掉`source/fonts`中相关文件，并在`./theme/landscape/source/css/_variables.styl`中的`font-icon-version`修改为最新的 Font Awesome 版本号。

然后，在`source/css/_partial/article.styl`中，找到以`.article-share-***`开头的代码，或添加或替换以下内容。
``` bash
.article-share-sina
  @extend $article-share-link
  &:before
    content: "\f18a"
  &:hover
    background: color-sina
    text-shadow: 0 1px darken(color-sina, 20%)

.article-share-qq
  @extend $article-share-link
  &:before
    content: "\f1d6"
  &:hover
    background: color-qq
    text-shadow: 0 1px darken(color-qq, 20%)

.article-share-renren
  @extend $article-share-link
  &:before
    content: "\f18b"
  &:hover
    background: color-renren
    text-shadow: 0 1px darken(color-renren, 20%)

.article-share-tencent
  @extend $article-share-link
  &:before
    content: "\f1d5"
  &:hover
    background: color-tencent
    text-shadow: 0 1px darken(color-tencent, 20%)
```
最后，找到`source/css/_variables.styl`中`Colors`部分，最后四行分别为四个社交网站图标的背景色，可根据这些网站的主题色修改。可使用如下修改结果：
``` bash
color-sina = #ea0020
color-qq = #518adb
color-renren = #406ccb
color-tencent = #33b5eb
```

每个主题有很多不同的修改方法，关于 landscape 主题的更多修改可以查看[Hexo 主题 Landscape 改造小记](http://blanboom.org/hack-hexo-theme-landscape.html#toc_4)。

* Hexo设置分类和标签

大多数时候我们需要为我们所写的 blog 添加分类和标签，那么在 hexo 中应该怎么做呢？

每当我们通过`hexo new title`新创建一篇博文之后，博文的初始内容会如下图所示：

		title: test go
		date: 2015-06-12 16:14:38
		tags:
		---

可以编辑标题，日期和标签，并没有分类的选项，可以手动加入`categories`项。然后直接在相应的项后填入我们想要的内容即可。添加多个分类或标签的格式类似，如下所示：
		
		categories: [categories1,categories2,...]
		tags: [tag1,tag2,...]

当然，为了不必每次创建新的 blog 后手动添加`categories`项，我们可以修改模板内容，打开`/scaffolds/post.md`文件，加入`categories`项即可。

* Hexo更换主题

玩 blog 更换主题必然是很重要的一个方面，那么对于 Hexo来说，我们要怎么更换主题呢？本文以更换 Jacman 主题为例，更换其他主题类似。

首先，找到你想要的主题的地址，绝大多数 Hexo 的主题都托管在 Github 上，那么我们找到所想要主题的 repo url。使用 Git bash 进入到我们本地 blog 的文件夹，然后将主题 clone 到`/themes`目录下。

		$ git clone https://github.com/wuchong/jacman.git themes/jacman

然后，修改根目录下的`_config.yml`文件，找到`theme`属性并将其置为`jacman`。

		# Extensions
		## Plugins: http://hexo.io/plugins/
		## Themes: http://hexo.io/themes/
		theme: jacman                              # // 主题名称

然后，更新主题即可。

		cd themes/jacman
		git pull origin master

jacman主题提供了丰富的属性配置，可根据个人需要修改配置文件。详情请参考[Jack's Blog，如何使用Jacman主题](http://wuchong.me/blog/2014/11/20/how-to-use-jacman/)。

更多关于hexo的主题，可参考[Github Hexo Themes](https://github.com/hexojs/hexo/wiki/themes)，[知乎，有哪些好看的hexo主题](http://www.zhihu.com/question/24422335)等等。

### 总结

这篇博文整合了几份优秀的关于 Hexo 的资源，相应的也已经在文中给出了链接，尽管并没有一些创新的地方，但还是希望能对同学们有一些帮助。