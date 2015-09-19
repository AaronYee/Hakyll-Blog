---
title: Github page + Hexo ，独立博客我们来了
tags: hexo,github,技术杂谈
---

忽然萌生了要写博客的想法，折腾了一天，总算搭配好了环境。这篇文章并不是很详细的教程，但作为一个刚刚实践过的人，我会把我搭配过程中遇到的种种问题在这里讲解出来，希望能对一些同学有所帮助。当然，我同样会在文章中给出实现过程中参考的blog，一知半解的同学可以进行参考。

先说一下我的搭配环境，并没有购买独立域名，而是采用了Github为Github page所分配的二级域名，所以对于想拥有独立blog而又想free of charge的话，那么接着看下去。

<!--more-->

### 准备工作，What we need？

---

* [Github 账户](https://github.com/)
* [Git Shell，windows环境下我使用了Git bash](https://msysgit.github.io/)
* [Node.js](https://nodejs.org/)
* 文本编辑器，windows下推荐[Notepad++](https://notepad-plus-plus.org/) & [Sublime](http://www.sublimetext.com/)


### 创建与配置Github

---

注册Github的过程这里不再多说，不明白的同学可以参考[如何搭建一个独立博客——简明Github Pages与Hexo教程](http://cnfeat.com/2014/05/10/2014-05-11-how-to-build-a-blog/)一文。



#### 配置SSH key
---

老实的讲，我还并没有搞懂SSH key的作用。Someone say 是为了建立local与remote的联系，但是如果不手动配置SSH key，github系统同样会为我们默认生成一个。但为了避免出错，我们还是按部就班的做吧，生命在于折腾。。下面的部分参考[BeiYuu's blog](http://beiyuu.com/github-pages/)。

**现在已经明白配置 SSH key 的作用，如果不配置 SSH key，我们每次上传文件至 remote 端的话都需要输入用户名和密码，而配置了 SSH key 之后，我们每次只需要填入设置的密码即可。**

首先，检查电脑上现有的ssh key，文件存放位置通常在 **“C:\Users\username\ .ssh”** 文件夹中。

然后，生成新的ssh key，在git bash中输入下列命令：

``` bash
$ ssh-keygen -t rsa -C "邮件地址@youremail.com"
Generating public/private rsa key pair.
Enter file in which to save the key (/Users/your_user_directory/.ssh/id_rsa):  Click ENTER
```
点击回车后，系统会要求输入密码串：
``` bash
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
```
输入两次密码，看到下图后，标明ssh key设置成功。
![](/assets/images/hexogit/sshkeyset.png)

接下来，添加ssh key到Github端。打开**“C:\Users\username\ .ssh”** 文件夹中**"id_rsa.pub"**文件，可使用notepad++或者sublime文本编辑模式，复制全部内容。登陆Github账户后，点击右上角粉红色按钮，选择settings。
![](/assets/images/hexogit/setting.png)

进入**personal settings**，选择**SSH keys**，点击**Add SSH key**，将复制的内容粘贴到key中，单击**Add key**即可完成添加。
![](/assets/images/hexogit/sshsetting.png)

在git bash中输入以下命令，测试是否添加成功。
``` bash
$ ssh -T git@github.com
Enter passphrase for key '/c/Users/Limbo/.ssh/id_rsa':
Hi ! You've successfully authenticated, but Github does not provide shell access.
```

#### 创建Github page
---
首先登陆Github账户，然后我们便可以创建我们的blog主页了（其实本质上就是一个仓库repository）。点击右上角加号create new repository，如下图所示，
![](/assets/images/hexogit/createRepo.png)
Repository name请填入`ownername.github.io`，必须注意的是，**Repository name必须与Owner名字一致**。例如此处对于我来说，需填入`AaronYee.github.io`。其他项不需调整，点击create repository完成创建。

接下来测试一下，引用[Github page](https://pages.github.com/)官方主页的例子，首先打开git bash进入工作目录（任意指定），clone下我们刚刚在github端创建好的repository，命令如下：
![](/assets/images/hexogit/gitclone.png)

将其中的**username**那么替换为你的**github name**即可，也可以从repository页面找到clone地址，在github端进入指定repository，
![](/assets/images/hexogit/repository.png)
点击右侧Copy to clipboard即可复制URL地址。其他选项如上图所示的Clone in Desktop和Download ZIP也同样可以使用。

然后进入本地clone下的repository文件夹，并创建html文件，如下图所示：
![](/assets/images/hexogit/createhtml.png)

Go on，将编辑好的文件上传回Github服务器端。命令如下所示：
![](/assets/images/hexogit/gitadd.png)

关于Git命令这里不再过多阐述，可参考[Git教程](http://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000)，[Pro Git](http://git-scm.com/book/zh/v1)。

提交成功后，可打开浏览器地址栏输入 **http://username.github.io** （username替换为你的repository name）查看是否可以显示出刚才所设置的html文件内容，若成功显示，则证明Github page搭建成功。第一次通常会有一些**延时**，请耐心等待10分钟左右时间。另外请注意，github的**邮箱验证**可能会影响到Github page的搭建，请及时验证邮箱。

**Okay，至此，Github端环境搭建完成。**

### 安装Hexo
---
在安装Node.js的过程中，**请不要修改默认的安装路径**，因为涉及到环境变量的配置问题。成功安装Node.js与Git bash后，在Git bash中输入下述命令即可安装hexo。

``` bash
$ npm install -g hexo-cli
```

注意，如果在Git bash中提示`npm command not found`，请切换到windows command中进行安装。

hexo安装完成后，可以创建我们用于写blog的文件夹了，anywhere you want。创建好后，在git bash中输入如下命令，其中`<folder>`为我们刚刚所创建的文件夹。

``` bash
$ hexo init <folder>      // Initialization，初始化
$ cd <folder>
$ npm install             // 安装插件
```

打开我们刚刚所建立的文件夹，会发现其中多出了很多内容，这些便是hexo所依赖的信息，具体内容如下所示：
```
.
├── _config.yml        // 配置文件
├── package.json       // 应用程序的信息
├── scaffolds          // 模板文件夹
├── scripts            // 脚本文件夹
├── source             // 资源文件夹
|   ├── _drafts
|   └── _posts
└── themes             // 主题文件夹
```

因为我们在写博客的时候，编辑的文件是**“.md”**文件，而在部署到blog的时候，需要生成为**html**文件，这个过程可由下述过程完成。
``` bash
$ hexo generate        // 最新版本的hexo支持简化形式，即 hexo g
```
执行上述命令后，在我们的blog文件夹中会自动生成一个public文件夹，这个文件夹的内容即是我们需要部署到blog服务器端的内容。接下来，输入下述命令开启本地服务器。
``` bash
$ hexo server        // 最新版本的hexo支持简化形式，即 hexo s
```
打开浏览器，地址栏中输入**"http://localhost:4000"**，若弹出下列界面，则证明配置成功。
![](/assets/images/hexogit/sample.png)

现在我们已经完成了本地端的配置，那么接下来**怎样将我们本地写好的blog挂载到服务器上呢**？So easy，用我们上文配置好的**Github page**，这就相当于将我们本地写好的文件上传到Github repository中，然后便可以在Github page下浏览到我们在本地写好的blog了。

上传的过程，我们可以将public文件夹中的所有内容复制到clone下的repository文件夹中，并通过git命令上传。但是，hexo已经帮我们集成好了这个操作。我们只需要配置好环境，便可以实现一键部署。首先，打开我们创建的blog文件夹下，用文本编辑器打开`_config.yml`文件，在最下方找到**Deployment**选项，将其配置成如下的形式即可。
``` bash
# Deployment
## Docs: http://hexo.io/docs/deployment.html
deploy:
  type: git
  repo: https://github.com/username/username.github.io.git
  branch: master
```
其中的**username**替换为个人的**repository name**。配置完成后，我们即可通过命令一键将所写的内容部署到服务器端。
``` bash
$ hexo deploy       // 最新版本的hexo支持简化形式，即 hexo d 
```
部署过程中会要求我们输入github的用户名和密码，正确输入即可。部署成功后，再次打开浏览器，进入我们上文搞定的Github page界面，**http://username.github.io**，即可看到我们本地写好的文件已经可以成功访问了！

当我们想新写一篇博客的时候，在git bash改变到blog目录的情况下，输入以下命令
``` bash
$ hexo new [layout] <title>       //  layout默认使用_config.yml中的default_layout参数代替，此处可以为空。
```
即可发现`./source/_posts`文件夹中多出了一个`<title>.md`文件，使用文本编辑器编辑该文件，按照MarkDown语法格式，即可完成blog的编写。

### 配置Hexo
---

Hexo的配置文件集中在主目录下的`_config.yml`文件中，下面贴出个人的配置文件和注释，可以根据个人的需要进行修改。

``` bash
# Hexo Configuration
## Docs: http://hexo.io/docs/configuration.html
## Source: https://github.com/hexojs/hexo/

# Site
title: Aaron-Yee Blog                       // 网站标题
subtitle: 专注 & 沉淀                        // 网站副标题
description:                                // 网站描述
author: Aaron Yee                           // 作者名字
language: zh-CN                             // 网站使用的语言
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
source_dir: source                          // 资源文件夹，用来存放内容
public_dir: public                          // 公共文件夹，用于存放生成的站点文件
tag_dir: tags                               // 标签文件夹
archive_dir: archives                       // 归档文件夹
category_dir: categories                    // 分类文件夹
code_dir: downloads/code                    // include code 文件夹
i18n_dir: :lang                             // 国际化(i18n)文件夹
skip_render:                                // 跳过指定文件的渲染

# Writing                                   // 设置hexo new 时候的相关配置
new_post_name: :title.md                    // 新文章文件名称 # File name of new posts                
default_layout: post                        // 预设布局
titlecase: false                            // 把标题转换为title case # Transform title into titlecase
external_link: true                         // 在新标签中打开链接 # Open external links in new tab
filename_case: 0                            // 把文件名称转换为(1)小写或(2)大写
render_drafts: false                        // 显示草稿
post_asset_folder: false                    // 启动Asset文件夹
relative_link: false                        // 把链接改为与根目录的相对位置
future: true                                // 显示未来的文章
highlight:                                  // 代码块设置
  enable: true
  line_number: true
  auto_detect: true
  tab_replace:

# Category & Tag                            // 分类 & 标签
default_category: uncategorized
category_map:
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
theme: jacman                              // 主题名称

# Deployment                               // 自动部署的配置
## Docs: http://hexo.io/docs/deployment.html
deploy:
  type: git
  repo: https://github.com/AaronYee/AaronYee.github.io.git
  branch: master
```
更多关于Hexo的信息可以在[hexo](http://hexo.io/zh-cn/)中查看。

### 更换Hexo主题
---

很显然，玩blog，主题是很重要的一个方面，那么怎么样**更换Hexo的主题**呢？本文以**jacman**主题为例，下文转自[Jack's Blog，如何使用Jacman主题](http://wuchong.me/blog/2014/11/20/how-to-use-jacman/)。

首先，使用Git bash进入本机的blog根目录，然后执行以下命令。

``` bash
$ git clone https://github.com/wuchong/jacman.git themes/jacman
```
Jacman 需要安装 Hexo 2.7 及以上版本，请先升级您的 Hexo 程序，再启用此主题。

然后，修改根目录下的`_config.yml`配置文件中的`theme`属性，将其设置为`jacman`。
``` bash
# Extensions
## Plugins: http://hexo.io/plugins/
## Themes: http://hexo.io/themes/
theme: jacman                              // 主题名称
```

然后更新主题
``` bash
cd themes/jacman
git pull origin master
```

jacman主题提供了丰富的属性配置，可根据个人需要修改配置文件。详情请参考[Jack's Blog，如何使用Jacman主题](http://wuchong.me/blog/2014/11/20/how-to-use-jacman/)。

更多关于hexo的主题，可参考[Github Hexo Themes](https://github.com/hexojs/hexo/wiki/themes)，[知乎，有哪些好看的hexo主题](http://www.zhihu.com/question/24422335)等等。

### 总结
---
总结一下实践过程中遇到的几个问题，希望能对后来的同学有所帮助。

* **Q. 上传本地repository到github端时，执行命令`git remote add origin`时出现 fatal: remote origin already exists 错误。**
  > 请先执行命令`git remote rm origin`，然后再重新添加。
* **Q. 上传本地repository到github端时，执行命令`git push origin master`时出现 error: failed to push som refs to... 错误。**
  > 可执行命令 `git pull origin master` 将远程文件拉下来再push。
* **Q. 打开`http://localhost:4000`只看到一堆代码，并没有预想中的网页出现。**
  > 这可能是由于hexo并没有对网页代码进行动态解析，请在git bash的blog根目录下重新输入`npm install`生成依赖的插件包。
* **Q. 打开`username.github.io`的时候，并没有显示出于本地server浏览同样的效果。**
  > 有部分原因可能是Github有延迟的原因，请稍后再试。若还是出现问题，请细心检查配置文件`_config.yml`。
* **Q. 使用Jacman主题，修改配置文件后并没有出现预想的效果。**
  > 注意修改配置文件时，`_config.yml`文件中的每个属性值前必须留一个空格。请务必注意缩进问题，尽量保持与原文档格式一致，相应项对齐。
* **Q. Blog内容中想加入配图，图片文件应该放在哪个文件夹中。**
  > Markdown插入图片的格式为`![](图片地址){ImgCap}图片标题{/ImgCap}`，外部链接图片直接在图片地址中填入，本地图片可在本地blog根目录的`./source/`文件夹中新建一个文件夹images用来存放图片，然后插入图片时图片地址为`/imgages/Fig1.png`。