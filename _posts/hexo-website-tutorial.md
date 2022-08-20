---
title: 超详细：这个网站，到底是怎么做出来的？
date: 2022-08-16 19:20:27
tags: 
- GitHub
- Website
- Hexo
categories:
- [ GitHub,Pages ]
---

断更好久了，今天终于抽空来写一点。不知不觉之间，这个网站已经上线运行1年多了，于是，我就开了这个新坑（`Hexo`网站的配置以及深度开发），应该够我写一阵子了，也算作送给这1年来的present……我也会随着教程的更新重复一遍过程，以保证内容的正确性。

顾名思义，这篇文章就记录一下我在开发这个网站时的操作过程，以及可能会遇见的一些问题。你可以在我的基础上继续深入，自由发挥！好了，闲话少说，我们这篇超详细的`Hexo`网站教程，马上开始！  

**注：本教程所用平台是`Win10`，其他系统可能有细微差别~由于涉及到`GitHub`，建议先参照[3个小妙招](https://guleixibian2009.github.io/2021/08/14/3%E4%B8%AA%E5%B0%8F%E5%A6%99%E6%8B%9B%E5%8A%A0%E9%80%9F%E4%BD%A0%E7%9A%84GitHub/)来加个速！**

<!--more-->

## 1. 准备工作部分

### 1.1 你~~可能~~一定会用到的那些软件

为了使用`Hexo`这个强大的框架，我们需要先安装一些依赖，还有一些其他的编程软件。为了真的把这个教程变得“新手向”一点，我就把你需要的软件都列在了这里：

| 类别          | 必要性              | 名称                                                                |
| ----------- | ---------------- | ----------------------------------------------------------------- |
| 依赖          | 高                | `NodeJS`                                                          |
| 编程相关、配置网站参数 | 中高               | （推荐）`VSCode`、`Sublime Text`以及任何你用着顺手的编辑器                          |
| 文章相关        | 中~~（你甚至可以用记事本）~~ | （推荐）`Marktext`（开源免费）、`Typora`（付费）                                 |
| 命令行         | 高                | `Windows Terminal Preview`（集成终端，支持自定义）、`Git`（需要配置`SSH`连接，暂时请先自己搜） |

**注：如果你使用`chocolatey`，你可以尝试先用命令行安装！** 这些软件我们依次来说：

#### 1.1.1 `NodeJS`

`NodeJS`是一款很流行的`JavaScript`运行时（环境），也是使用`Hexo`的必装依赖。打开[安装官网](https://nodejs.org/en/)，如下图，推荐选择左侧的长期支持版本（`LTS`版本）。

![](https://s1.ax1x.com/2022/08/16/v04OaV.png)

安装之后，打开命令行，输入：

```powershell
node -v
npm -v
```

来检测是否安装成功。如果都可以成功返回版本号，那么你就可以进行下一步操作了！

> 注：一般情况下，官方下载源会很慢，我们需要给`NodeJS`修改镜像源。使用
> 
> ```powershell
> npm config set registry http://registry.npm.taobao.org/
> ```
> 
> 来调整为国内镜像源。

#### 1.1.2 `Markdown`编辑器`Marktext`

![](https://s1.ax1x.com/2022/08/16/v057WD.png)

周知所众，我们写博客一般都是用`Markdown`这种标记语言的（不会写？参见这篇[`Markdown`教程]()）。纯净的界面，即时的渲染、开源与免费三大特点让我爱上了这款编辑器。别的咱也不说，好不好用你自己说了算！这个项目的开源地址在`GitHub`上：<https://github.com/marktext/marktext/>，之后怎么安装我就不用说了吧。

#### 1.1.3 `Windows`终端·预览版

如果你嫌`CMD`或者`Powershell`的界面、字体不合你的心意，或者就想尝试一些新功能，你可以试一下`Windows Terminal Preview`。它把几个终端都打包在了一起，且支持自定义界面和启动位置等，同时可以分屏。

![](https://s1.ax1x.com/2022/08/17/vBcCg1.png)

你可以在`Microsoft Store`中下载到这款终端·预览。另外，需要改一下`powershell`的执行策略，管理员权限执行：

```powershell
Set-ExecutionPolicy Bypass
```

即可。

#### 1.1.4 `hexo`，你网站的框架

上面的软件都准备好了吗？我们来安装博客框架罢。在`powershell`中执行：

```powershell
npm install -g hexo-cli
```

就可以全局安装这个框架了。安装好之后，重启命令行，并用`hexo`命令检测是否安装成功：

![](https://s1.ax1x.com/2022/08/17/vBWTOI.png)

### 1.2 你的`repo`与服务器

我们来到`GitHub`，并新建一个仓库，名称叫作`{username}.github.io`。如果你曾跟着之前的文章做过`Jekyll`版网站、`master`分支被占用的话，你可以新建一个`hexo`分支。注意需要勾选`LICENSE`和`README`，这样可以形成一个`master`分支。

![](https://s1.ax1x.com/2022/08/17/vB4wY8.png)

之后，你就会得到类似这样的一个页面：

![](https://s1.ax1x.com/2022/08/17/vB5y9O.png)

然后我们转到`Settings`，启用（修改）`GitHub Pages`的相关设置，选择`Deploy from a branch`后勾选你的目标分支。如果你完全跟着我来的，默认是`master`；如果你以前动用过这个仓库，则切换到你新的分支上。如下图，点击`Save`就可以触发一次更新：

![](https://s1.ax1x.com/2022/08/17/vB563D.png)

稍等片刻（大概1~3分钟）后，访问`https://{username}.github.io`，如果显示的不是下面这个灰色的`404`，那么我们就可以开始下一步了！

![](https://s1.ax1x.com/2022/08/17/vDVNFI.png)

> 注：我曾经在`Jekyll`那篇文章中说过，`GitHub Pages`会在每一次`commit`之后触发一次更新`action`，即自动化。由于需要在服务器上进行操作，可能会出现”排队“的情况，如果设置没错却迟迟出不来”非404“页面，我想，你可能需要继续等一等……

## 2. 初始化、主题与一些设置

### 2.1 让`Hexo`运行起来！

接下来我们就来让`Hexo`发挥一下它的威力罢。找到一个合适的文件夹，然后执行下面这条命令来初始化一个`Hexo`项目（这里以我自己为例，自己修改文件夹名）：

```powershell
hexo init hexo_website_tutorial //换上自己的文件夹名
```

正常情况下你获得到如下的结果：

![](https://s1.ax1x.com/2022/08/17/vDamKe.png)

这个时候，我们`cd`看一下都创建了哪些东东：

```
.
├─.github
├─node_modules
├─scaffolds
├─source
│  └─_posts
└─themes
```

简要说明一下：`.github`文件夹可以直接无视；`node_modules`是一些`hexo`本身的依赖；`scaffolds`里放了一些模板`Markdown`，暂且不用管它；`source`文件夹中会放我们的文章；`themes`文件夹则是为之后应用主题做准备。还有一个`_config.yml`文件，是我们网站的配置文件。

那么，我们怎么生成一个静态的网站呢？此时我们就要用到`hexo generate`（简称`hexo g`）命令了。它会读取我们写的文章，配合着主题设置生成静态文件，并复制二进制文件（图片、音频等）。注意，为了网站资源链接可以正确工作，我们要在`_config.yml`文件中改一行，是你网站的链接：

![](https://s1.ax1x.com/2022/08/18/vrkW28.png)

修改好之后，执行截图：

![](https://s1.ax1x.com/2022/08/18/vDXL8A.png)

执行之后，我们会发现多了一个`public`文件夹和`db.json`文件。`public`文件夹会在生成静态文件之后复制到这里，方便上传；`db.json`是网站的一些`meta`信息，可以不用管。

生成完了，我们一定会想看一看生成后的效果。你可以使用`hexo server`命令在`4000`端口上启动一个服务器。为了方便，你可以加一个参数`-o`来自动打开浏览器。如下：

```powershell
hexo s -o
```

在`4000`端口上，我们的默认网站样式类似这样：

![](https://s1.ax1x.com/2022/08/18/vDXOgI.png)

此时这个主题叫做`landscape`。由于我个人有更喜欢的主题（`NeXT`）并且`landscape`主题可以开发的部分不多，我们不会使用这款主题。稍后你就会知道如何切换主题。

### 2.2 部署到服务器

想让别人看到我们的网站，我们就要更新`GitHub`上的仓库，触发部署`action`。可是，我不希望每一次都要用3条`git`命令来上传，怎么办？一个好消息是，`hexo`提供给我们一个`deploy`命令。

#### 2.2.1 远程仓库参数设置

当然了，`hexo`此时也不知道我们的仓库在哪里，对吧。这时候配置文件`_config.yml`就可以派上用场了。我们找到它的`Deploy`部分，并添加一些配置：

![](https://s1.ax1x.com/2022/08/18/vrCnyj.png)

具体格式如下：

```yaml
# Deployment
deploy:
    type: 'git'
    repo: git@github.com:{username}/{repo_name}.git
    branch: {branch_name}
```

然后，我们来试一下`hexo d`这个命令……

![](https://s1.ax1x.com/2022/08/18/vriuaq.png)

诶，为什么会这样呢？`Deployer not found`是什么意思？原来，我们还需要安装一个官方插件：`hexo-deployer-git`。

#### 2.2.2 `hexo-deployer-git`

我们在网站根目录下执行这个命令：

```powershell
npm i hexo-deployer-git --save
```

然后再执行`hexo d`（太长了，不用图片了）：

```
INFO  Validating config
INFO  Deploying: git
INFO  Setting up Git deployment...
Initialized empty Git repository in D:/08 网站/hexo_website_tutorial/.deploy_git/.git/
[master (root-commit) 0b3e2b7] First commit
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 placeholder
INFO  Clearing .deploy_git folder...
INFO  Copying files from public folder...
INFO  Copying files from extend dirs...
[master 3a2b089] Site updated: 2022-08-18 17:47:15
 18 files changed, 5172 insertions(+)
 create mode 100644 2022/08/17/hello-world/index.html
 create mode 100644 archives/2022/08/index.html
 create mode 100644 archives/2022/index.html
 create mode 100644 archives/index.html
 create mode 100644 css/fonts/FontAwesome.otf
 create mode 100644 css/fonts/fontawesome-webfont.eot
 create mode 100644 css/fonts/fontawesome-webfont.svg
 create mode 100644 css/fonts/fontawesome-webfont.ttf
 create mode 100644 css/fonts/fontawesome-webfont.woff
 create mode 100644 css/fonts/fontawesome-webfont.woff2
 create mode 100644 css/images/banner.jpg
 create mode 100644 css/style.css
 create mode 100644 fancybox/jquery.fancybox.min.css
 create mode 100644 fancybox/jquery.fancybox.min.js
 create mode 100644 index.html
 create mode 100644 js/jquery-3.4.1.min.js
 create mode 100644 js/script.js
 delete mode 100644 placeholder
Enumerating objects: 34, done.
Counting objects: 100% (34/34), done.
Delta compression using up to 8 threads
Compressing objects: 100% (26/26), done.
Writing objects: 100% (34/34), 882.39 KiB | 1.49 MiB/s, done.
Total 34 (delta 3), reused 0 (delta 0), pack-reused 0
remote: Resolving deltas: 100% (3/3), done.
To github.com:Guleixibian2009/hexo-website-tutorial.git
 + 5066890...3a2b089 HEAD -> master (forced update)
branch 'master' set up to track 'git@github.com:Guleixibian2009/hexo-website-tutorial.git/master'.
INFO  Deploy done: git
```

如果出现类似的结果，那我们就已经部署成功了。这个时候我们去`GitHub`上去，稍等一会后并访问你的网站看一下，你应该可以看到和本地端口上完全一样的页面。

![](https://s1.ax1x.com/2022/08/18/vrkDDH.png)

### 2.3 切换到`NexT`主题

当我们可以成功的部署到`GitHub`上去后，我们就可以开始切换主题了。我们要用的这个主题叫做`NexT`，准确的说，是`Gemini`子主题。为了使用这个主题，我们在根目录下克隆一下`GitHub`上面的主题仓库`theme-next/hexo-theme-next`：

```powershell
git clone https://github.com/theme-next/hexo-theme-next themes/next
```

![](https://s1.ax1x.com/2022/08/19/vrxxmt.png)

然后打开根目录下的`_config.yml`（有区别于之后我们会用到主题内的`_config.yml`文件，切勿搞混）：

![](https://s1.ax1x.com/2022/08/19/vrzSTf.png)

修改过后重新生成一遍静态文件（`hexo clean`+`hexo g`），打开本地端口（`hexo s -o`）可以看见，我们已经切换到`NexT`的`Muse`子主题了：

![](https://s1.ax1x.com/2022/08/19/vrzDcd.png)

实际上，`NexT`主题分别是有4个子主题的。打开`themes/next`文件夹下（简称主题文件夹下`_config.yml`），找到95行，可以看到所有子主题，以及黑夜模式的设置（本人并未开启）：

![](https://s1.ax1x.com/2022/08/19/vrzynI.png)

要切换到`Gemini`子主题，只需把第100行注释掉，并取消注释第103行即可。我们重新生成一下（还记得那3条命令吧）：

![](https://s1.ax1x.com/2022/08/19/vspsTP.png)

主题是切换过来了，可是我看着怎么是英文的呢？或者，感觉东西太少了？还有，为什么我叫`John Doe`？别急，下一步，便是设置一些`metadata`。

### 2.4 网站信息设置

在网站根目录下的`_config.yml`的开头，你可以看到这样的几条配置：

![](https://s1.ax1x.com/2022/08/19/vsp6Ff.png)

详细地解释一下（我自己先修改了）：`title`、`subtitle`、`description`、`author`、`language`几项在更改后会改变下图中的对应位置，`description`、`keywords`、`language`、`timezone`几项则是变成了网站`metadata`。（<kbd>Ctrl+I</kbd>应该可以查看）

![](https://s1.ax1x.com/2022/08/19/vs9EXd.png)

![](https://s1.ax1x.com/2022/08/19/vs9ZnA.png)

~~（可能做得有些丑，谅解下哈）~~

> 回顾：`hexo`常用命令（以后我就不会再提醒咯）
> 
> - 清除生成缓存——`hexo clean`。（对主题上的混乱或配置未生效有帮助）
> 
> - 生成静态文件——`hexo g`。
> 
> - 部署到远程服务器——`hexo d`。
> 
> - 打开本地服务器端口——`hexo s`。
> 
> 教你几个小妙招：
> 
> - `hexo d`和`hexo g`其实可以合并成一个命令，叫做`hexo g -d`，就可以自动先生成在自动部署。
> 
> - `hexo s`加上参数`-o`就可以自动在浏览器中打开端口。

## 3. `Gemini`子主题的官方配置......

现在我们就可以给我们的网站添加一些功能与细节了。先打开本地端口，让我们从左往右说：

### 3.1 左侧的侧边栏

左边较窄的竖栏叫`sidebar`（侧边栏），分为上下两部分，上半部分是一个导航栏，存放了一些站内链接；下半部分是关于你、一些网站统计数据、友情链接，这里也是我们可以自定义的地方（非官方的插件，如音乐、天气等，我们在第5节非官方插件中说）。当你打开一片博客后，下半部分也可以作为一个文章目录。下面几张图供参考：

![](https://s1.ax1x.com/2022/08/19/vsihCV.png)

![](https://s1.ax1x.com/2022/08/19/vsi43T.png)

#### 3.1.1 添加更多的站内链接

仔细研究主题`_config.yml`，你会找到这样一个区块，正是关于站内链接的：

![](https://s1.ax1x.com/2022/08/19/vsFpKe.png)

看起来，我们目前有两个可用链接（主页、归档），相对应的就是`home`和`archive`。

##### 3.1.1.1 添加链接

我们来试试取消注释`about`、`tags`和`categories`：

![](https://s1.ax1x.com/2022/08/19/vskVoR.png)

诶，正好，同步增加了三个链接~~（不过暂时打不开）~~！那我们是不是就能总结出来填入的格式了？

```yml
menu:
    key: /link/ || icon
```

`key`指的是链接的名字（不代表链接地址，这个名字后面还会有用），一个冒号，然后是链接地址（可相对可绝对），然后是`||`标识符，后面跟一个`font-awesome`图标名（只能用免费版的）。

掌握了语法之后，我们就可以尝试添加一个自己的链接了！假设你新建了一个歌单页面（具体操作参见后面第4节文章相关操作），它的链接是`/album/`，并且想要用`font-awesome`中`fas fa-compact-disc`这个图标，那我们就可以在配置文件中添加这样一行：

```yml
menu:
    album: /album/ || fas fa-compact-disc
```

在你重新生成之前，你突发奇想想要把它放在主页那个链接下面，该怎么办呢？我发现，你只需要把这一行移动到`home`那一行后面即可：

```yml
menu:
  home: / || fa fa-home
  album: /album/ || fas fa-compact-disc
  about: /about/ || fa fa-user
  tags: /tags/ || fa fa-tags
  categories: /categories/ || fa fa-th
  archives: /archives/ || fa fa-archive
  #schedule: /schedule/ || fa fa-calendar
  #sitemap: /sitemap.xml || fa fa-sitemap
  #commonweal: /404/ || fa fa-heartbeat
```

效果类似这样：

![](https://s1.ax1x.com/2022/08/19/vskeF1.png)

可是，明明其他链接都有中文，怎么新加的`album`就没有？

##### 3.1.1.2 调整`i18n`

别忘了，`NexT`主题的默认语言是英文！我们是通过修改配置强制翻译成中文的（可以回顾一下2.4节）。那...我们能不能手动翻译（学名`internationalization`，国际化，简称`i18n`)呢？其实是可以的。我们找到这个文件：

![](https://s1.ax1x.com/2022/08/19/vsA5gf.png)

然后我们重新生成，是不是就成功了呢？

![](https://s1.ax1x.com/2022/08/19/vsA48P.png)

记住这个方法，我们之后也还是会用到的！

##### 3.1.1.3 计数小“徽章”

想要显示目前我们的博客内一共有几篇文章、几个分类和几个标签吗？我们可以用一个`badge`解决这件事。还是刚才那段配置，有没有在下面看到一段这样的选项？

```yml
menu_settings:
  icons: true
  badges: false
```

我们把`badges`选项调成`true`，系统就会自动计数了。看一下效果：

![](https://s1.ax1x.com/2022/08/19/vsVzBF.png)

嗯，光荣的`0 0 1`。当然现在我们的“标签”页还是打不开的。具体怎么调文章的分类或如何创建“标签”页面等，我会在第4节文章相关操作中讲到。

#### 3.1.2 更新“综合信息中心”

我之所以把这个侧边栏的下半部分称作一个“综合数据中心”，主要是因为你几乎可以在这里放任何你想放的信息，比如你的头像、个性签名、文章相关统计、个人链接等等。（至于天气和音乐播放器我们之后会在第5节非官方插件中讲到。）这是我的网站目前的样子：

![](https://s1.ax1x.com/2022/08/19/vsEUsS.png)

##### 3.1.2.1 你的头像

想要给大家展示一下你的头像吗？当然可以。准备好一张照片（建议方形或圆形），移动到`/public/images`这个文件夹里。然后打开主题配置文件，找到如下配置：

![](https://s1.ax1x.com/2022/08/19/vsEaqg.png)

```yml
# Sidebar Avatar
avatar:
  # Replace the default image and set the url here.
  url: /images/avatar.gif
  # If true, the avatar will be dispalyed in circle.
  rounded: true
  # If true, the avatar will be rotated with the cursor.
  rotated: true
```

`url`是你图片的路径，格式就是`/images/`再加上文件名（不一定是`avatar.gif`）。`rounded`则是选择是否要显示为圆形，`rotated`是选择是否要在鼠标移动到图片上时旋转。我们看一下效果如何：

![](https://s1.ax1x.com/2022/08/19/vsENM8.png)

注：这个黑色的`N`就是`/images/`文件夹下的`logo.svg`。

##### 3.1.2.2 个人链接

既然说了，这里是“综合信息中心”，那我能不能放一点个人信息（个人链接）呢？当然是可以的。最终的效果如下：

![](https://s1.ax1x.com/2022/08/20/vsY8B9.png)

那这个是在哪里设置的呢？我们可以找到这样一段配置：

![](https://s1.ax1x.com/2022/08/20/vsYYA1.png)

```yml
social:
  GitHub: https://github.com/Guleixibian2009 || fab fa-github
  E-Mail: mailto:guleixibian2009@outlook.com || fa fa-envelope
  RSS: https://guleixibian2009.github.io/hexo-website-tutorial/atom.xml || fa fa-rss
  Website: https://guleixibian2009.github.io/ || fab fa-html5
```

它的语法和`3.1.1.1`节中链接的语法是相同的，这里就不再赘述了。

##### 3.1.2.3 `Creative Commons`文章版权声明

是开源项目总得有个开源许可证`LICENSE`吧。像博客一类非代码开源项目，我们一般选用`CC`版权声明。一共有6种形式（当然还有其他较特殊的协议，比如放弃权利`CC0`，可以自行搜索）：

| 协议                 | `by`（`Attribution`） | `nc`（`Noncommercial`） | `nd`（`No Derivative Works`） | `sa`（`Share Alike`） |
| ------------------ | ------------------- | --------------------- | --------------------------- | ------------------- |
| 转载时必须标示原作者         | √                   | ×                     | ×                           | ×                   |
| 标示原作者，且禁止修改        | √                   | ×                     | √                           | ×                   |
| 标示原作者，且禁止商用        | √                   | √                     | ×                           | ×                   |
| 标示原作者，且禁止修改、商用     | √                   | √                     | √                           | ×                   |
| 标示原作者，且禁止商用，必须相同协议 | √                   | √                     | ×                           | √                   |
| 标示原作者，必须相同协议       | √                   | ×                     | ×                           | √                   |

一般我们选用`CC by-nc-sa`这种协议。那么，我们如何直观地向别人展示呢？`NexT`主题内置了小图标的功能，可以找到这一部分配置文件：

![](https://s1.ax1x.com/2022/08/20/vsYG7R.png)

```yml
creative_commons:
  license: by-nc-sa
  sidebar: true
  post: false
  language: deed.zh
```

我们选中`sidebar`一项，`NexT`就会自动渲染出一个小图标了。至于`post`一项，我们放到3.2节中讲。`language`如果需要调整为中文，直接填写`deed.zh`即可。看一下渲染效果：

![](https://s1.ax1x.com/2022/08/20/vsY3nJ.png)

#### 3.1.3 文章目录

如果你现在进入那篇默认的`Hello World`文章，你可以在原先“信息中心”的地方看到文章的目录。那么这个目录有没有可以自定义的地方呢？也是有的。我们可以找到对应的配置：

![](https://s1.ax1x.com/2022/08/20/vsdROO.png)

```yml
toc:
  enable: true
  # Automatically add list number to toc.
  number: true
  # If true, all words will placed on next lines if header width longer then sidebar width.
  wrap: false
  # If true, all level of TOC in a post will be displayed, rather than the activated part of it.
  expand_all: false
  # Maximum heading depth of generated toc.
  max_depth: 6
```

仔细观察一下生成的`toc`（`Table Of Contents`，简称`toc`），发现每一个标题都被自动编上了号。可是，这就对像我这种习惯手动编号的人很不友好啊，我们就可以把`number`这个选项关掉。`wrap`则是说过长的标题是全部显示还是省略号，我选择了全部显示。`expand_all`指要不要全部展开，如果启用的话就会显示所有标题，然而像我这篇非常长的文章明显是不太合适的，所以就保持在`false`上。这样它就只会显示当前浏览部分的目录了。`max_depth`是指要生成多少层标题（1~6）。如果你不想显示过于细致的标题，可以调小。那调整之后效果类似这样：

![](https://s1.ax1x.com/2022/08/20/vsdfmD.png)

### 3.2 文章板块相关配置

终于到了我们的重头戏。有一个美观的`sidebar`只是基础，博客最重要的就是`post`（即博文部分）了。官方提供的自定义不多，但还是有可以打开的功能的。（注：在3.2节中我们只会讲关于这一板块的功能，并不会讲到类似“阅读全文按钮”等。我们把它留在第4节文章相关配置里讲。）

#### 3.2.1 文章相关信息

如果你细心的观察过文章标题下的小字，你就会发现诸如发布时间、更新时间、本文字数、分类等信息。而是否显示它们都是可以调的。

![](https://s1.ax1x.com/2022/08/20/vsgC9g.png)

##### 3.2.1.1 基本配置

你可以在这里找到一些基本配置：

![](https://s1.ax1x.com/2022/08/20/vsgP3Q.png)

```yml
# Post meta display settings
post_meta:
  item_text: true
  created_at: true
  updated_at:
    enable: true
    another_day: true
  categories: true
```

看起来现在所有功能都是打开的。`item_text`指的是要不要显示数据名称；`created_at`是发布时间；`categories`是文章的分类。由于默认的`Hello World`文章是没有分类的，所以它就没有显示。可是，为什么我没有看到字数统计等信息呢？原来这是通过另外一项设置实现的。

##### 3.2.1.2 字数统计

就在`post_meta`一节下面，有一个`symbols_count_time`。

![](https://s1.ax1x.com/2022/08/20/vsgicj.png)

```yml
symbols_count_time:
  separated_meta: true
  item_text_post: true
  item_text_total: false
```

用之前我们
