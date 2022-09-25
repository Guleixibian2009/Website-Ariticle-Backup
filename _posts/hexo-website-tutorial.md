---
title: 超详细：这个Hexo网站，到底是怎么做出来的？
date: 2022-08-16 19:20:27
tags: 
- GitHub
- Website
- Hexo
categories:
- [ GitHub,Pages,Hexo ]
---

断更好久了，今天终于抽空来写一点。不知不觉之间，这个网站已经上线运行1年多了，于是，我就开了这个新坑（`Hexo`网站的配置以及深度开发），应该够我写一阵子了，也算作送给这1年来的present……我也会随着教程的更新[重复一遍过程](/hexo-website-tutorial)，以保证内容的正确性。

顾名思义，这篇文章就记录一下我在开发这个网站时的操作过程，以及可能会遇见的一些问题。你可以在我的基础上继续深入，自由发挥！好了，闲话少说，我们这篇超详细的`Hexo`网站教程，马上开始！  

**注：本教程所用平台是`Win10`，其他系统可能有细微差别~由于涉及到`GitHub`，建议先参照[3个小妙招](https://guleixibian2009.github.io/2021/08/14/3%E4%B8%AA%E5%B0%8F%E5%A6%99%E6%8B%9B%E5%8A%A0%E9%80%9F%E4%BD%A0%E7%9A%84GitHub/)来加个速！**

<!--more-->

---

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

稍等片刻（大概1~3分钟）后，访问`https://{username}.github.io`（这就是你的网站域名了），如果显示的不是下面这个灰色的`404`，那么我们就可以开始下一步了！

![](https://s1.ax1x.com/2022/08/17/vDVNFI.png)

> 注：我曾经在`Jekyll`那篇文章中说过，`GitHub Pages`会在每一次`commit`之后触发一次更新`action`，即自动化。由于需要在服务器上进行操作，可能会出现”排队“的情况，如果设置没错却迟迟出不来”非404“页面，我想，你可能需要继续等一等……

---

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
> - `hexo d`和`hexo g`其实可以合并成一个命令，叫做`hexo g -d`，就可以自动先生成再自动部署。
> 
> - `hexo s`加上参数`-o`就可以自动在浏览器中打开端口。

---

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

| 协议                 | `by`（`Attribution`） | `nc`（`NonCommercial`） | `nd`（`No Derivative Works`） | `sa`（`Share Alike`） |
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

用之前我们还需要安装一个依赖，叫做`hexo-symbols-count-time`。直接使用`npm`安装即可：

```powershell
npm i hexo-symbols-count-time --save
```

然后我们来看一下这些设置有什么用。`item_text_post`指的是要不要在文章标题下方显示本文字数&阅读时间；`item_text_total`则是在页脚显示全站计数。我们重新渲染来看一下效果：

![](https://s1.ax1x.com/2022/08/20/vsI96U.png)

![](https://s1.ax1x.com/2022/08/20/vsIplT.png)

#### 3.2.2 代码块样式

在默认的`Hello World`文章中，有4个代码块。也许你不喜欢这种较亮的主题；或者，你不介意主题，但只是想要添加一个复制按钮？这一切的一切都是可以修改的！我们找一下对应的配置，嗯，在这里：

![](https://s1.ax1x.com/2022/08/20/vsIim4.png)

```yml
codeblock:
  # Code Highlight theme
  highlight_theme: normal
  # Add copy button on codeblock
  copy_button:
    enable: true
    # Show text copy result.
    show_result: true
    # Available values: default | flat | mac
    style: default
```

高亮是默认开启的（没人不用这个功能，你真的不用的话到根目录`_config.yml`中`# Writing`一节可以禁用）。你可以自己选一个喜欢的`highlight_theme`，我保留了`normal`，也就是浅色。`copy_button`中直接两个都调成`true`就可以显示复制按钮了。效果如下：

![](https://s1.ax1x.com/2022/08/20/vsICXF.png)

#### 3.2.3  看见了还真不一定知道是什么的辅助功能

为了直观地展示这一节的内容，我将先超纲新建一篇文章，大家见谅哈。在这篇文章里既有中文又有英文，我还给了它一个标签，一个分类。

##### 3.2.3.1 中英文空格——`Pangu`

![](https://s1.ax1x.com/2022/08/20/vsT5f1.png)

我个人觉得中、英文混杂时没有个空格很难受，有的时候又会忘记加（就是假设，假设！）。怎么办呢？`NexT`提供一个功能叫做`Pangu`。它可以自动在中英文之间添加空格。我们找到配置：

![](https://s1.ax1x.com/2022/08/20/vsTTl6.png)然后改成`true`即可。渲染一下试试：

![](https://s1.ax1x.com/2022/08/20/vsT4YR.png)

##### 3.2.3.2 图片懒加载——`lazyload`

一路看下来，有没有发现博客中的图片都是启用了懒加载的？就在`pangu`的配置附近，有一个：

```yml
# Vanilla JavaScript plugin for lazyloading images.
# For more information: https://github.com/ApoorvSaxena/lozad.js
lazyload: false
```

改成`true`即可。它的原理就是先获取较快的占位图，再在滚动时加载新的图片。效果如下：

![](https://gcdnb.pbrd.co/images/62i8BHj3vjF7.gif?o=1)

（是动图，压缩过，点击重新播放）

##### 3.2.3.3 图片放大——`fancybox`

想要实现一个图片点击放大功能吗？`fancybox`可以满足你的需求。我们找到这样一段配置：

```yml
# FancyBox is a tool that offers a nice and elegant way to add zooming functionality for images.
# For more information: https://fancyapps.com/fancybox
fancybox: false
```

改成`true`之后我们来看一下效果：

![](https://s1.ax1x.com/2022/08/20/vsToSx.png)

##### 3.2.3.4 局部刷新——`pjax`

想要快速的切换页面？启用`pjax`即可。可能很多人听说过`ajax`，其实`pjax`相当于类似的功能。

启用之前需要先用`git`克隆`theme-next-pjax`的仓库。

```powershell
git clone https://github.com/theme-next/theme-next-pjax themes/next/source/lib/pjax
```

然后在配置文件中启用`pjax`：

![](https://s1.ax1x.com/2022/08/20/vsqaj0.png)

效果图我就不放了，动图上传起来太麻烦，得另找图床。可以自己试一下效果。

#### 3.2.4 数学公式支持——`mathjax`

如果你看过这篇[关于`LaTex`的文章](https://guleixibian2009.github.io/2021/11/28/Markdown中Latex常用语法/)的话，你可能会知道，`Markdown`文章中是可以添加数学公式的。那么，`Hexo`有没有渲染数学公式的功能呢？是有的。我们可以找到如下配置：

![](https://s1.ax1x.com/2022/08/21/vycLss.png)

当然注释里也说得很清楚了，我们需要安装另一个`hexo`编译器，即`hexo-renderer-kramed`。使用如下两个命令：

```powershell
npm un hexo-renderer-marked
npm i hexo renderer-kramed --save
```

安装即可。将`enable`那一行改为`true`，这个时候你就已经准备好`MathJax`了，来测试一下：

$$
f(x) =
\begin{cases}
x^2 \qquad & x \gt 0 \\
e^x \qquad & x \le 0
\end{cases}
$$

不过，使用`hexo-renderer-kramed`会带来一个小问题...

#### 3.2.5 修复`Todo List`无法渲染的问题

这个问题是我在写`Markdown`语法那篇文章时发现的。虽然`Todo List`不是一个非常重要的语法，但我想我们最好还是修复一下这个问题：

![](https://s1.ax1x.com/2022/08/27/vR74PS.png)

解决办法是，打开`node_modules/hexo-renderer-kramed/lib/renderer.js`，并在第19行添加以下内容（对，就是查到的）：

```js
// Support To-Do List
Renderer.prototype.listitem = function(text) {
  if (/^\s*\[[x ]\]\s*/.test(text)) {
    text = text.replace(/^\s*\[ \]\s*/, '<input type="checkbox" disabled="disabled"></input> ').replace(/^\s*\[x\]\s*/, '<input type="checkbox" disabled="disabled" checked></input> ');
    return '<li style="list-style: none">' + text + '</li>\n';
  } else {
    return '<li>' + text + '</li>\n';
  }
}; 
```

修改之后重新渲染一遍即可。还是来测试一下：

- [x] 这是一个`Todo List`。
- [ ] 这是一个未被勾选的选项。

#### 3.2.6 文末板块配置

在文章末尾一般会放置一些关于文章的额外的信息。这是我的博客文末的功能：

![](https://s1.ax1x.com/2022/08/28/vW2L2q.png)

##### 3.2.6.1 版权声明方框

很重视要告诉你的读者这是你的原创文章，或者觉得有必要强调自己使用了`Creative Commons`声明？可以考虑添加一个版权方框。至于设置的话，在这里：

![](https://s1.ax1x.com/2022/08/28/vW2U81.png)

把`post: false`调整为`true`即可。重新生成一下，看一下效果：

![](https://s1.ax1x.com/2022/08/28/vW2Y59.png)

当然，如果你对默认的翻译不满意的话，可以找到之前那个`i18n`配置文件，然后自行修改。

![](https://s1.ax1x.com/2022/08/28/vW2NCR.png)

##### 3.2.6.2 修改标签的小图标

仔细看，在文章末尾会显示出这篇文章的标签。在上一节的图片中，它的样式是`# Test`。我个人不喜欢这个`#`，想把它换掉。有这个功能吗？可以找到如下配置：

![](https://s1.ax1x.com/2022/08/29/vfFMzd.png)

把`tag_icon`一项改成`true`，然后重新渲染一下看看：

![](https://s1.ax1x.com/2022/08/29/vfFniD.png)

##### 3.2.6.3 其他发布渠道链接（引流）

需要在文章末尾给自己其他的发布渠道（如公众号，`CSDN`等）或其它前端项目引流吗？我们同样可以添加一个链接方框。这是添加后的效果：

![](https://s1.ax1x.com/2022/08/29/vfFuJe.png)

我们可以找到这样的配置：

![](https://s1.ax1x.com/2022/08/29/vfFKRH.png)

```yml
# Subscribe through Telegram Channel, Twitter, etc.
# Usage: `Key: permalink || icon` (Font Awesome)
follow_me:
  #Twitter: https://twitter.com/username || fab fa-twitter
  #Telegram: https://t.me/channel_name || fab fa-telegram
  #WeChat: /images/wechat_channel.jpg || fab fa-weixin
  #RSS: /atom.xml || fa fa-rss
```

它的语法和3.1.1.1节的是一样的，可以参考一下。同时，如果你觉得老是修改`i18n`很烦的话，可以直接用你想要的名字作为`Key`，如：

```yml
follow_me:
  #Twitter: https://twitter.com/username || fab fa-twitter
  #Telegram: https://t.me/channel_name || fab fa-telegram
  #WeChat: /images/wechat_channel.jpg || fab fa-weixin
  RSS: /atom.xml || fa fa-rss
  旧版网站: https://guleixibian.github.io/ || fab fa-html5
  手写网站: https://guleixibian2009.github.io/Hand-Written-HTML-Site/ || fas fa-laptop-code
  Awesome-Bootstrap项目: https://guleixibian2009.github.io/awesome-bs5/ || fab fa-bootstrap
```

##### 3.2.6.4 打赏功能

在自己的网站上加几个打赏二维码还是一个不错的选择~~（当然我其实没有放）~~，包括一些项目`README`里面也会放。预先准备好几个收款码（一定是固定的那种）或者你想放的图片，放到`themes/next/source/images`文件夹中。找到这样的配置：

![](https://s1.ax1x.com/2022/08/29/vfBut0.png)

```yml
# Reward (Donate)
# Front-matter variable (unsupport animation).
reward_settings:
  # If true, reward will be displayed in every article by default.
  enable: false
  animation: false
  #comment: Donate comment here.

reward:
  #wechatpay: /images/wechatpay.png
  #alipay: /images/alipay.png
  #paypal: /images/paypal.png
  #bitcoin: /images/bitcoin.png
```

这个打赏的配置有两部分。`reward_settings`是设置打赏按钮；图片地址要写在`reward`里面。先把`enable`调成`true`，然后添加几张图片试试：

```yml
reward_settings:
  # If true, reward will be displayed in every article by default.
  enable: true
  animation: false
  comment: 给作者买一杯作业...

reward:
  #wechatpay: /images/wechatpay.png
  #alipay: /images/alipay.png
  #paypal: /images/paypal.png
  #bitcoin: /images/bitcoin.png
  把我的网站分享给别人吧！: /images/websiteQR.png
```

至于`comment`一行的话，是你想要在打赏按钮上方显示的句子。看一下效果：

![](https://s1.ax1x.com/2022/08/29/vfBnkq.png)

### 3.3 网站上的小“零件”

这一章是关于页面上的一些（官方的）小功能。比如说（并不是所有的）：

![](https://s1.ax1x.com/2022/08/29/vfD88f.png)

#### 3.3.1 页脚信息显示

页脚（`footer`）也是稍微有一些可以调整的地方的：

![](https://s1.ax1x.com/2022/08/29/vfDG28.png)

我们目前的页脚是这样的：

<img title="" src="https://s1.ax1x.com/2022/08/29/vfD3PP.png" alt="" data-align="inline">

看起来有一个版权符号，年份，作者名，还有一个爱心。但实际上，版权年份其实只会显示当前年份。如果想像我一样显示类似2021~2022，该如何实现呢？我们可以找到这样一段配置：

![](https://s1.ax1x.com/2022/08/29/vfDJxS.png)

具体来讲一下：

1. 被注释掉的一行`since`指的是站点建立的时间。把它取消注释，并改为现在的年份，就可以每年更新了（每年要重新渲染一次）。

2. 想要让爱心动起来的话，可以把`icon`中`animated`改为`true`。

3. 版权默认使用项目名称，但如果希望使用我自己的名字，可以在`copyright`中写上自己的名字。

4. `powered`指要不要显示“由`Hexo`强力驱动”，默认打开。

5. `beian`中是网站`ICP`备案，我没备案就不写上了。修改完后，记得重新渲染一下。

那个计数是怎么实现的呢？那是一个第三方服务，我放在第5章中讲。

#### 3.3.2 回到顶部按钮

看完一篇非常长的文章，如果读者想要一键返回顶部，我们就需要一个`back2top`按钮。基本款的默认已经有了，但是我们还可以对它进行进一步配置。

![](https://s1.ax1x.com/2022/08/30/vhUJyj.png)

这里一共有3个选项。`enable`默认开启；`sidebar`指的是按钮的位置要不要加在侧边栏下方；`scrollpercent`是显示阅读百分比。我开启了第三项。最终效果：

![](https://s1.ax1x.com/2022/08/30/vhU8Sg.png)

#### 3.3.3 阅读进度条

如何让读者清晰地看出自己已经读了多少呢？刚刚显示百分比的功能还是不错的。不过我们还有更加直观一些的方法——阅读进度条。找到这段配置：

![](https://s1.ax1x.com/2022/08/30/vhUGlQ.png)

```yml
# Reading progress bar
reading_progress:
  enable: true
  # Available values: top | bottom
  position: top
  color: "#37c6c0"
  height: 3px
```

如果你不介意进度条的颜色和高度的话，直接`enable: true`就已经可以用了。不满意的话可以自己调整一下下面三个参数。这是最终的效果：

![](https://s1.ax1x.com/2022/08/30/vhU1fS.png)

#### 3.3.4 书签功能

需要在关闭页面时记录下自己的阅读进度吗？可以打开（自动）书签功能。找一下：

![](https://s1.ax1x.com/2022/08/30/vhdkKH.png)

直接把`enable`调成`true`即可。默认的版本是`auto`，即关闭页面自动保存；你也可以调成`manual`，只在读者点击图标时保存。效果如下（自己尝试一下吧）：

![](https://s1.ax1x.com/2022/08/30/vhdC8O.png)

#### 3.3.5 右上角`GitHub`徽标

虽然我们已经在侧边栏中加过一个`github`链接了，但我们同样可以用一个更加明显的方式为自己的`github`账号引流。这就是大名鼎鼎的`GitHub Banner`。至于配置的话，就在刚才的下面：

![](https://s1.ax1x.com/2022/08/30/vhdArd.png)

```yml
# `Follow me on GitHub` banner in the top-right corner.
github_banner:
  enable: true
  permalink: https://github.com/Guleixibian2009
  title: Follow me on GitHub~
```

打开功能，先把`enable`调成`true`。`permalink`是指向你想要引流的链接（比如`github`账号，项目地址等），`title`是鼠标移到图标上时显示什么。来试一下：

![](https://s1.ax1x.com/2022/08/30/vhdixe.png)

不过如果细看的话...这个`banner`和书签在页面顶部时似乎有点小bug。重叠我能接受，可是露出一个角来就有点奇怪了啊！

![](https://s1.ax1x.com/2022/08/30/vhdP2D.png)

我研究了一下，可以把书签的`CSS`中`right`属性调到`25px`就好了。找一下`/themes/next/source/css/_common/outline/header/bookmark.styl`文件...不太确定这是什么语言，但是不怕！找到上面那个`right`（第5行那个）把那个变量名称改成`25px`即可了。这样就不会重叠了。

![](https://s1.ax1x.com/2022/08/30/vhdEqA.png)

> 另及：使用这个变量的本意应该是想让书签的右侧和`b2t`按钮右侧宽度相同，但我觉得`5px`应该不太看的出来吧。

#### 3.3.6 加载进度条——`pace`

注意到网站上加载时的蓝色加载条了吗？

![](https://s1.ax1x.com/2022/08/30/vhfg2j.png)

这个进度条是基于`pace`做出来的。首先我们需要克隆`pace`的仓库：

```powershell
cd themes/next
git clone https://github.com/theme-next/theme-next-pace source/lib/pace
```

然后找到对应的配置：

![](https://s1.ax1x.com/2022/08/30/vhf2xs.png)

```yml
# Progress bar in the top during page loading.
# Dependencies: https://github.com/theme-next/theme-next-pace
# For more information: https://github.com/HubSpot/pace
pace:
  enable: true
  # Themes list:
  # big-counter | bounce | barber-shop | center-atom | center-circle | center-radar | center-simple
  # corner-indicator | fill-left | flat-top | flash | loading-bar | mac-osx | material | minimal
  theme: minimal
```

我用的是`minimal`。重新渲染一下，看一下效果吧。

#### 3.3.7 网站图标——`favicon`

直到现在我们网站的图标还是那个黑色的`N`。能不能改一个好看一点的呢？先找一个自己喜欢的图标，然后转成`ico`格式的文件（可以用`convertio`试试）。复制两份，分别命名`16x16.ico`和`32x32.ico`。拖到`themes/next/source/images`文件夹里面。然后我们找到对应的配置：

![](https://s1.ax1x.com/2022/09/01/v5LMNj.png)

```yml
favicon:
  small: /images/16x16.ico
  medium: /images/32x32.ico
  #apple_touch_icon: /images/apple-touch-icon-next.png
  #safari_pinned_tab: /images/logo.svg
  #android_manifest: /images/manifest.json
  #ms_browserconfig: /images/browserconfig.xml
```

只保留`small`和`medium`，再把文件名填进去即可。

---

## 4. 文章相关配置

现在我们已经把基本的一些配置好了。我们可以开始添加一些文章、页面~~（心心念念的标签、分类页）~~，还可以有搜索、`404`页面等。你会学到如何给文章添加标签、分类等等。

### 4.1 关于博客——`post`

如果你曾注意过`scaffolds`文件夹里的内容，你会看到`Hexo`一共有3种“类型”，分别是`post`博客、`page`页面和`draft`草稿。我不太习惯用草稿功能，就把它放过喽。我们先来把博客讲一下：

#### 4.1.1 新建一篇文章

还记得3.2.3节中我超纲建文章吗？建文章的命令是`hexo new`。如下：

```powershell
hexo new a-new-post
```

然后我们就可以在`source/_post`里面找到一个`a-new-post.md`。打开看看：

![](https://s1.ax1x.com/2022/08/30/vh5OMj.png)

文件几乎是空白的，只有一小段`YML`（学名`YAML Front Matter`）。这里面存放着关于这篇文章的元信息：

```yml
title: a-new-post
date: 2022-08-30 17:02:10
tags:
```

默认是有三个字段的，即`title`、`date`和`tags`。`title`会先默认设置为文件名，你可以改成这篇文章的标题（比如“4.1.1节新建文章示例”）。`date`建议不要改，是你新建文章的时间。`tags`是这篇文章的标签。先在文章内部写点东西试试渲染一下。我现在修改成这样，渲染一下看看：

```md
---
title: 4.1.1节新建文章示例
date: 2022-08-30 17:02:10
tags:
---

Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut 
labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris 
nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit 
esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt 
in culpa qui officia deserunt mollit anim id est laborum.
```

![](https://s1.ax1x.com/2022/08/30/vh5xZq.png)

#### 4.1.2 标签与分类

现在我们尝试给文章添加一些标签和分类（照例，用`Test`）。只需在`Front Matter`中加一点即可：

```yml
title: 4.1.1节新建文章示例
date: 2022-08-30 17:02:10
tags: 
- Test1
- Test2
categories:
- [Test1, Test2]
- Test3
```

可以看到我们添加了一个`categories`字段。先讲标签：新建一行，然后用`-`打头，空格，然后输入分类名，可以重复多行。`categories`中是差不多的，可是这个`- []`是用来干嘛的呢？这代表分类下的子分类。待会新建分类`page`时你就会看出来它的效果。渲染一下看看：

![](https://s1.ax1x.com/2022/08/30/vhH89f.png)

（为了一张图放完，这张图片是80%比例下的截图的）

#### 4.1.3 主页节选——`excerpt`

我们新加的博客内容都是很短的，可以完整的放在主页上。可像我这种几k字的，主页完全放不下啊！这是我们就可以使用节选功能，同时会自动显示一个按钮，提示“继续阅读”。语法如下：

```md
This is a piece of text. It's going to be very long.

<!--more-->

Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut 
labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris 
nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit 
esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt 
in culpa qui officia deserunt mollit anim id est laborum.
```

没错，只要在你想分开的地方加一个`<!--more-->`即可。我们拿`Hello World`那篇文章试一下：

![](https://s1.ax1x.com/2022/08/30/vhH14P.png)

#### 4.1.4 文章置顶

在我的网站主页上有一篇置顶的序言，就像书的`preface`一样。`Hexo`文章在主页上的排列顺序（默认）是按发布时间后往前（即越新越往上）排布的，如何打破这个规则，强制在最上方呢？一开始我也没有查到对应的设置（都是手写进去代码），不过在翻看`hexo`的生成代码时（不太具体知道这是什么语言，似乎是`mozilla`开发的`nunjucks`），我注意到有一个`sticky`选项（而且似乎值是个数字），在这里：

![](https://s1.ax1x.com/2022/08/31/v4LWTJ.png)

```
{%- if post.sticky > 0 %}
  <span class="post-sticky-flag" title="{{ __('post.sticky') }}">
    <i class="fa fa-thumbtack"></i>
  </span>
{%- endif %}
```

然后我就找到一篇`post`，在`Front Matter`里面加上这么一行：

```yml
sticky: 1
```

诶，神奇的是就好了！我在`_config.yml`中没有看到任何和`sticky`有关的配置，没想到自己摸索出来了。看一下最后的效果：

![](https://s1.ax1x.com/2022/08/31/v4LRw4.png)

#### 4.1.5 分页功能

目前来说，我们的主页上可能还没有几篇文章。可是，设想一下将来，当你有了几十篇博客（只是设想），难道还得全部一股脑的堆在主页上吗？我们可以尝试加一个分页功能。即：每满设定的文章数就会自动生成主页的下一页。先看一下效果吧，我是6篇一分：

![](https://s1.ax1x.com/2022/08/31/v4OXuT.png)

找一下如下的配置（注意在`Hexo`配置文件内，切勿搞混了）：

![](https://s1.ax1x.com/2022/08/31/v4OLvV.png)

看起来是默认打开的啊？那我就把数值减小一点，改成6就好了。

### 4.2 关于页面——`page`

在3.1.1.1节中我们在侧边栏中添加了标签页、分类页，还有一个歌单的链接。这一章我们会把这些页面补齐，并给网站添加一个`404`页面。

#### 4.2.1 新建页面

新建页面和新建一篇博客的命令是差不多的。如下，只需要在`new`后面添加一个`page`：

```powershell
hexo new page tags
```

`tags`就是所有标签页。可是，执行这个命令到底会发生什么呢？我们来看一下`source`文件夹。多了一个`tags`文件夹，里面有一个`index.md`。打开看看：

![](https://s1.ax1x.com/2022/09/02/vIRp9g.png)

嗯，和`post`差不多，一个时间一个标题，只是没有标签和分类。然后，看一下渲染的效果，有没有这个页面了：

![](https://s1.ax1x.com/2022/09/02/vIRCcj.png)

但这个样子肯定是有`bug`的。第一，它的标题怎么叫`tags`？第二，之前链接列表中既然有这个默认的`tags`，那它为什么不是自动化的，不可能连统计标签的功能都没有吧！别急，马上就把这个功能加进来，只需要一行`Front Matter`，再把标题改下：

```yml
title: 所有标签
type: tags
```

试一下渲染效果：

![](https://s1.ax1x.com/2022/09/02/vIR93Q.png)

似乎好了耶！然后类似的，我们加一下分类、关于和歌单页，把`tags`分别换为`categories`、`about`、`album`即可。别忘了改页面的标题，并给分类页加上`type: categories`！这是最后的效果：

![](https://s1.ax1x.com/2022/09/03/voSauR.png)

至于`about`和`album`页的话，可以放自己想放的东西。

> 另及：还记得我们在4.1.2节中给文章添加了一个`- []`嵌套分类吗？现在你应该可以理解这是什么意思了吧：它表示分类下的子分类，比如“编程”，“编程-`Python`”等等。同时支持更多层嵌套。

#### 4.2.2 `404`页面

`404`页面和之前的页面做起来很相似。还是用`hexo new page 404`这个命令来新建出页面，然后我们来添加一些配置：

```yml
title: ''
date: 2021-08-15 16:28:02
comments: false
sitemap: false
permalink: /404
```

`title`设为空，这样就不会显示标题。`comments: false`表示不在本页上加载`Gitalk`，详见第5章。`sitemap: false`表示不把本页加入站点地图，详见第6章。最重要的是这个`permalink`，它会声明：这个页面是通用`404`页面。往里面加上一些提示性的句子，比如：

```md
# 404 Not Found 您访问的页面走丢了！

将于10秒后返回 [首页](https://guleixibian2009.github.io/hexo-website-tutorial) ......
```

渲染出来就是这样：

![](https://s1.ax1x.com/2022/09/03/vo9hh8.png)

##### 4.2.2.1 自动跳转功能

上面的代码块里提到了10秒后返回主页。这个是靠下面一段代码实现的：

```html
<script language="javascript" type="text/javascript"> 
    setTimeout("javascript:location.href='/'", 10000); 
</script>
```

我曾经在`Jekyll`那篇文章里面提到过，还记得吗？直接把它粘贴到`index.md`末尾即可。重新渲染，可以自己去看一下效果。

### 4.3 关于搜索——`searchdb`

当我们网站上的文章渐渐多起来后，我们就需要一个方便读者找到对应文章的方式，这就是一个搜索功能。我们先安装一下对应的`package`：

```powershell
npm i hexo-generator-searchdb --save
```

不同的是，我们不能直接去找主题`_config.yml`内的配置，而是得先在博客配置内添加这样的配置，添在底部即可：

```yml
# Local Search
search:
  path: search.xml
  field: post
  format: html
  limit: 10000
```

随后我们再去找这一段配置：

![](https://s1.ax1x.com/2022/09/03/voAu79.png)

```yml
# Local Search
# Dependencies: https://github.com/theme-next/hexo-generator-searchdb
local_search:
  enable: false
  # If auto, trigger search by changing input.
  # If manual, trigger search by pressing enter key or search button.
  trigger: auto
  # Show top n results per article, show all results by setting to -1
  top_n_per_article: 1
  # Unescape html strings to the readable one.
  unescape: false
  # Preload the search data when the page loads.
  preload: false
```

先把`enable`调成`true`，就可以开启功能了。然后看到`top_n_per_article`的选项，意思是说每篇博客显示几个结果。可以调大一点，比如调成5。我们来看一下渲染的效果。

![](https://s1.ax1x.com/2022/09/03/voAZXF.png)

![](https://s1.ax1x.com/2022/09/03/voAmm4.png)

然后顺便讲一下那个提示语是怎么改的。找到`i18n`文件，如下：

![](https://s1.ax1x.com/2022/09/03/voAn0J.png)

把`placeholder`改成你想要的提示语即可。

### 4.4 如何对`README`和`LICENSE`禁用渲染

也许你已经发现，我们在第1节中创建的`README`和`LICENSE`都已经被覆盖，找不到了，就连`commit`都消失的无影无踪。不过，经过我的尝试，我们还是有办法添加回它们的。我们先复制这两个文件进`source`文件夹，然后找到主题配置：

![](https://s1.ax1x.com/2022/09/03/voA590.png)

看到那行`skip_render`了吗？我们用一个列表来代表禁用渲染的文件：

```yml
skip_render: [README.md, LICENSE]
```

`[]`就表示一个列表，每个文件名用逗号隔开即可。看一下渲染之后会发生什么：

![](https://s1.ax1x.com/2022/09/03/voAhhq.png)

这样，我们的`README`就不会被渲染成`HTML`了。以上这些，就是我们所有的较为基础的配置与文章相关的内容了。接下来我们会涉及到一些更高级的功能，使用到第三方插件，可以自己选择。

---

## 5. 第三方插件配置

写到这文章已经很长了，将近20k字了。不管怎么样，我们来继续我们的教程，~~争取再写20k啊~~。

### 5.1 动态背景

读了这么久的文章了，不会还没注意到我的动态背景吧。在背景上有50个点，随机游走，相互靠近时就会连成一条线。靠近鼠标时则会被“困住”，直到再次移动鼠标。这叫做`canvas_nest`。

> 另及：`next`其实有官方的动态背景，但我个人不满意，所以搜到了这一款。它曾经被集成入`Next`，但现在已不默认被集成，所以我把它归在第三方插件中。

我们先安装对应的插件，在`themes/next`文件夹下执行：

```powershell
git clone https://github.com/theme-next/theme-next-canvas-nest source/lib/canvas-nest
```

随后我们需要新增一段`yml`，加在主题配置文件内，随便加在哪里。不过便于后期修改，我把它和其他动态背景放在一起。

![](https://s1.ax1x.com/2022/09/03/voVwSP.png)

```yml
# Canvas Nest
# Dependencies: https://github.com/theme-next/theme-next-canvas-nest 
canvas_nest:
  enable: true 
  onmobile: true 
  color: '0,0,0' 
  opacity: 0.5 
  zIndex: -1 
  count: 50 
```

可以修改的有几个参数：`color`指线的颜色，配合`opacity`透明度使用；`zIndex`指图层，`-1`代表最下层；`count`代表最多同时出现多少条线。修改之后渲染即可。我特地给你们看一下效果：

![](https://s1.ax1x.com/2022/09/03/voVaWt.png)

### 5.2 侧边栏插件

总觉得侧边栏少了点东西，没有个性？我们可以尝试添加一些不同的东西......这是最后的效果：

![](https://s1.ax1x.com/2022/09/03/vo8YT0.png)

#### 5.2.1 外链播放器

音乐播放器的话是用的一个网易云的外链服务，好处在于方便（根本不需要登录什么的），快速（加载快播放也流畅）。我们先随便找一首歌（网页版的）：

![](https://s1.ax1x.com/2022/09/03/vo8Jwq.png)

##### 5.2.1.1 获取插件

看到上面的红色框框了吗？点进去，就是一个外链的生成界面：

![](https://s1.ax1x.com/2022/09/03/vo8eTP.png)

出于兼容性的考虑我们只能用`<iframe>`版的，`flash`已经过时了。首先我们要调整一个宽度，自己觉得合适就可以。不过不要过宽，否则待会会放不下。我自己选的是`280x66`。然后尽量不选自动播放吧，用户体验可能不会特别好，万一读者不喜欢这首歌怎么办？然后复制下面的代码就可以了，类似这样：

```html
<iframe frameborder="no" border="0" marginwidth="0" marginheight="0" width=280 height=86 src="//music.163.com/outchain/player?type=2&id=2080607&auto=0&height=66"></iframe>
```

注意一下另外两个红框，是两个相同的数字，即歌曲`id`。以后需要更改歌曲只要打开网页版后复制网址中的`id`并替换就可以了。

##### 5.2.1.2 调整侧边栏宽度

`Next`主题侧边栏的宽度默认是240，这个会有点窄，要调大一点。不是说一定要比插件的宽度长，短一点也可以，它会自动的缩短。然后我这边就选了260像素。看一下配置：

![](https://s1.ax1x.com/2022/09/03/vo8KfS.png)

##### 5.2.1.3 插入`swig`模板

到现在我们已经有了一个播放器，调了宽度，可是怎么把它插入到侧边栏里来呢？我们要到模板文件里去插。找到这个文件（`themes/next/layout/_partials/sidebar/site-overview.swig`），在105行左右（`CC`之后，`Blogroll`之前）插入代码即可：

![](https://s1.ax1x.com/2022/09/03/vo8uY8.png)

```jinja2
...

{%- if theme.creative_commons.license and theme.creative_commons.sidebar %}
  <div class="cc-license motion-element" itemprop="license">
  {%- set ccImage = '<img src="' + url_for(theme.images + '/cc-' + theme.creative_commons.license + '.svg') + '" alt="Creative Commons">' %}
    {{ next_url(ccURL, ccImage, {class: 'cc-opacity'}) }}
  </div>
{%- endif %}

<iframe frameborder="no" border="0" marginwidth="0" marginheight="0" width=280 height=86 src="//music.163.com/outchain/player?type=2&id=2080607&auto=0&height=66"></iframe>

{# Blogroll #}
{%- if theme.links %}
  <div class="links-of-blogroll motion-element">
    <div class="links-of-blogroll-title">
      {%- if theme.links_settings.icon %}<i class="{{ theme.links_settings.icon }} fa-fw"></i>{%- endif %}
      {{ theme.links_settings.title }}
    </div>
    <ul class="links-of-blogroll-list">
      {%- for blogrollText, blogrollURL in theme.links %}
        <li class="links-of-blogroll-item">
          {{ next_url(blogrollURL, blogrollText, {title: blogrollURL}) }}
        </li>
      {%- endfor %}
    </ul>
  </div>
{%- endif %}
```

最后我们来看一下渲染出来的效果：

![](https://s1.ax1x.com/2022/09/03/vo8nFf.png)

#### 5.2.2 天气插件

接下来是一个天气的插件。我们这个插件来自`tianqi.com`，它这个可以实时获取城市，不过原来是直接使用的，现在要关注什么公众号了，不过我可以直接把代码给大家。这是我当时获取到的代码：

```html
<iframe width="250" height="90" frameborder="0" scrolling="no" hspace="0" src="https://i.tianqi.com/?c=code&a=getcode&id=7&icon=1"></iframe>
```

目前还是可以正常运行的，不要求什么密码。我们还是找到`site-overview.swig`，把上面的代码粘贴到外链播放器下面去。看一下最终的效果：

![](https://s1.ax1x.com/2022/09/03/voJXLj.png)

### 5.3 不蒜子访客统计

需要一项服务来显示自己的客流量？`Next`中集成了`busuanzi`统计，虽然是第三方服务但也可以方便地添加到页面上。我们可以先看一下它的官网：

![](https://s1.ax1x.com/2022/09/04/voOrJH.png)

#### 5.3.1 启用功能

当然我们不用那么复杂，又一次在`swig`添加那么多代码，我们只要找到对应的配置勾选一下：

![](https://s1.ax1x.com/2022/09/04/voOgyt.png)

```yml
# Show Views / Visitors of the website / page with busuanzi.
# Get more information on http://ibruce.info/2015/04/04/busuanzi
busuanzi_count:
  enable: false
  total_visitors: true
  total_visitors_icon: fa fa-user
  total_views: true
  total_views_icon: fa fa-eye
  post_views: true
  post_views_icon: fa fa-eye
```

然后直接把所有的`false`改成`true`就可以拥有实时文章阅读量计数等功能。看一下最后的效果：

![](https://s1.ax1x.com/2022/09/04/voO6SA.png)

可是不对啊，我既然选了`post_views`，怎么不显示计数呢？于是我就去翻代码...

#### 5.3.2 翻`swig`，瞎折腾

![](https://s1.ax1x.com/2022/09/04/voOcQI.png)

在`themes/next/layout/_macro/post.swig`文件的120行找到这样的代码：

```jinja2
{%- if not is_index and theme.busuanzi_count.enable and theme.busuanzi_count.post_views %}
  <span class="post-meta-item" title="{{ __('post.views') }}" id="busuanzi_container_page_pv" 
style="display: none;">
    <span class="post-meta-item-icon">
      <i class="{{ theme.busuanzi_count.post_views_icon }}"></i>
    </span>
    <span class="post-meta-item-text">{{ __('post.views') + __('symbol.colon') }}</span>
    <span id="busuanzi_value_page_pv"></span>
  </span>
{%- endif %}
```

凭直觉来看，`if not is_index`很成问题啊！核理推测一下，是不是我们进入一篇文章就能看见`post_views`计数了？

![](https://s1.ax1x.com/2022/09/04/voOsWd.png)

果然。那在核理推测一下，是不是把`not is_index and`去掉，就可以在主页上显示了呢？我自己试了一下，发现这样会有`bug`，哪怕不看文章，也会出现计数的情况，个人没有想到特别好的解决方案，于是还是没有改。

### 5.4 相关文章插件

然后的话再讲一种引流的方式，这个相关文章插件。这算是一种站内引流吧。这个是最终的效果：

![](https://s1.ax1x.com/2022/09/04/vTMkRJ.png)

#### 5.4.1 安装与配置

照常我们先找到对应的配置。然后看一下需要的`dependency`：

![](https://s1.ax1x.com/2022/09/04/vTMZs1.png)

```yml
# Related popular posts
# Dependencies: https://github.com/tea3/hexo-related-popular-posts
related_posts:
  enable: false
  title: # Custom header, leave empty to use the default one
  display_in_home: false
  params:
    maxCount: 5
    #PPMixingRate: 0.0
    #isDate: false
    #isImage: false
    #isExcerpt: false
```

看起来我们需要安装`hexo-related-popular-posts`这个插件。安装过程中`npm`可能会提示你有部分`package`已被`deprecated`，不过不用管。安装后我们来改一下配置：

`enable`调成`true`之后就可以打开功能；`display_in_home`指要不要在主页上显示，我没开启；`title`、`maxCount`什么的，我放张图就懂了（另及：`isExcerpt`要求文章中一定出现`<!--more-->`手动分页，默认不会显示全文）：

![](https://s1.ax1x.com/2022/09/04/vTMAz9.png)

所以最后的配置类似这样：

```yml
# Related popular posts
# Dependencies: https://github.com/tea3/hexo-related-popular-posts
related_posts:
  enable: true
  title: 相关文章 为你推荐
  display_in_home: false
  params:
    maxCount: 3
    #PPMixingRate: 0.0
    isDate: true
    #isImage: false
    isExcerpt: true
```

不过我们现在由于多方面原因（标签、分类等）并不会生成。我们随便再创一篇文章，来点相同的标签啥的。我们重新渲染...出错了！`hexo g`会出现两个`ERROR`，但没有更多信息，而`hexo s`运行后，有的文章打不开，还出现如下错误：

```
Unhandled rejection Template render error: (D:\08 网站\hexo_website_tutorial\themes\next\layout\post.swig)
  Template render error: (D:\08 网站\hexo_website_tutorial\themes\next\layout\post.swig)
  Template render error: (D:\08 网站\hexo_website_tutorial\themes\next\layout\post.swig) [Line 19, Column 14]
  Template render error: (D:\08 网站\hexo_website_tutorial\themes\next\layout\post.swig)
  Template render error: (D:\08 网站\hexo_website_tutorial\themes\next\layout\_partials\head\head-unique.swig) [Line 10, Column 23]
  Template render error: (D:\08 网站\hexo_website_tutorial\themes\next\layout\post.swig) [Line 3, Column 3]
  Template render error: (D:\08 网站\hexo_website_tutorial\themes\next\layout\post.swig)
  Template render error: (D:\08 网站\hexo_website_tutorial\themes\next\layout\_partials\header\index.swig) [Line 6, Column 15]
  Template render error: (D:\08 网站\hexo_website_tutorial\themes\next\layout\post.swig)
  Template render error: (D:\08 网站\hexo_website_tutorial\themes\next\layout\_partials\header\sub-menu.swig) [Line 2, Column 29]
  Template render error: (D:\08 网站\hexo_website_tutorial\themes\next\layout\post.swig)
  Template render error: (D:\08 网站\hexo_website_tutorial\themes\next\layout\_partials\header\sub-menu.swig)
  Template render error: (D:\08 网站\hexo_website_tutorial\themes\next\layout\post.swig) [Line 5, Column 3]
  Template render error: (D:\08 网站\hexo_website_tutorial\themes\next\layout\post.swig) [Line 9, Column 12]
  Template render error: (D:\08 网站\hexo_website_tutorial\themes\next\layout\_macro\post.swig) [Line 214, Column 16]
  Template render error: (D:\08 网站\hexo_website_tutorial\themes\next\layout\_partials\post\post-related.swig)
  TypeError: config._d.getTime is not a function
    at Object._prettifyError (D:\08 网站\hexo_website_tutorial\node_modules\nunjucks\src\lib.js:36:11)
    at D:\08 网站\hexo_website_tutorial\node_modules\nunjucks\src\environment.js:563:19
    at Template.root [as rootRenderFunc] (eval at _compile (D:\08 网站\hexo_website_tutorial\node_modules\nunjucks\src\environment.js:633:18), <anonymous>:45:3)
    at Template.render (D:\08 网站\hexo_website_tutorial\node_modules\nunjucks\src\environment.js:552:10)
    at D:\08 网站\hexo_website_tutorial\themes\next\scripts\renderer.js:32:29
    at _View._compiled (D:\08 网站\hexo_website_tutorial\node_modules\hexo\lib\theme\view.js:136:50)
    at _View.render (D:\08 网站\hexo_website_tutorial\node_modules\hexo\lib\theme\view.js:39:17)
    at D:\08 网站\hexo_website_tutorial\node_modules\hexo\lib\hexo\index.js:64:21
    at tryCatcher (D:\08 网站\hexo_website_tutorial\node_modules\bluebird\js\release\util.js:16:23)
    at D:\08 网站\hexo_website_tutorial\node_modules\bluebird\js\release\method.js:15:34
    at RouteStream._read (D:\08 网站\hexo_website_tutorial\node_modules\hexo\lib\hexo\router.js:47:5)
    at Readable.read (node:internal/streams/readable:496:12)
    at resume_ (node:internal/streams/readable:999:12)
    at process.processTicksAndRejections (node:internal/process/task_queues:82:21)
```

似乎是什么获取时间时有`bug`。有办法修复吗？

#### 5.4.2 修复相关`bug`

经过多次尝试与搜索，我终于找到对应的解决方案。原文章参见“致谢”一节中的第5条。我们援引一下：

> 经过排查，本次发生错误是由 `hexo-related-popular-posts` 引发，在该库源码中使用 `moment` 初始化 `list.date` 导致了错误。 `list.date` 通过打印值可以看到是一个 `moment` 对象，但这个 `moment` 对象并不规范或者说可能在某处修改了这个 `moment` 对象的值。
> 
> `moment` 内部初始化有一段逻辑是:
> 
> ```js
> this._d = new Date(config._d != null ? config._d.getTime() : NaN);
> ```
> 
> 这个 `config` 就是 `moment(list.date)` 传入的 `list.date` 的值。`config._d` 是一个时间类型的字符串，并不是 `Date` 类型，因此没有 `getTime` 的方法。
> 
> 临时解决方法有两种，一是将 `isDate` 设为 `false`，也就是推荐列表中不展示时间。
> 
> 二是修改源码，做一层错误处理。从 `node_modules` 中打开文件(`/node_modules/hexo-related-popular-posts/lib/list-json.js`), 在编辑器中查找以下代码：
> 
> ```js
> if (inOptions.isDate && list.date != '') {
>     ret.date =  moment(list.date).format(config.date_format || 'YYYY-MM-DD')
> }
> ```
> 
> 修改为：
> 
> ```js
> if (inOptions.isDate && list.date != '') {
>     try {
>         ret.date =  moment(list.date).format(config.date_format || 'YYYY-MM-DD')
>     } catch(ex) {
>         ret.date =  moment(list.date._d).format(config.date_format || 'YYYY-MM-DD')
>     }
> }
> ```
> 
> 上述只是临时的解决方案，由于不好确定是哪一方的原因，也不想继续耗费太多精力在上面。

我个人也不是特别了解原理，不过这的确解决了我们的问题。大概在这里：

![](https://s1.ax1x.com/2022/09/04/vTMVMR.png)

然后便解决了。感谢`anran758`大佬。

### 5.5 评论系统

在写到这里的时候我有点犹豫，因为原来用的`GiTalk`由于某些网络原因（见下）挂掉了，又没有决定换什么，所以迟了好久。最后我选中的是来必力`livere`。

> **《论我捣鼓`GiTalk`的简要过程》**
> 
> 写到这里我本想去截图，结果一看启动不起来，没办法新建`issue`也没法登录`GitHub`账号。在排查了设置、网络的问题后，我发现有个致命的问题：`cors-anywhere.azm.workers.dev`被墙掉，然后`GiTalk`无法进行`GitHub oauth`，就不能用了。
> 
> 我于是尝试自己搭`worker`，结果发现是所有`Cloudflare worker`的链接都被墙掉了，然后我就彻底没招了，就只好作罢。不过......真的吗？
> 
> 后来我找到了`GiTalk`的仓库，里面有类似的`Issue`，甚至翻出了`CORS Anywhere`的仓库，找到了一个基于`Heroku`的备用`demo`链接。在一个`Issue`的[某条评论](https://github.com/Rob--W/cors-anywhere/issues/301#issuecomment-870990778)、[某条评论](https://github.com/Rob--W/cors-anywhere/issues/301#issuecomment-1012060775)中找到了一些备用链接。于是，就可以恢复正常了！
> 
> **另及：今年（2022）11月28号`Heroku`会关闭所有的免费服务，所以你看到类似`herokuapp.com`的链接都不用试了...**

最后的话成品是这样：

![](https://s1.ax1x.com/2022/09/07/vbFLZD.png)

#### 5.5.1 来必力`livere`

这个服务来自韩国，是韩语的页面，但是一旦应用到网站上就是中文的。到<https://livere.com>注册一个账号（你可能需要翻译），登录然后点击页首“安装”按钮，选择`city`版，填入链接什么的：

![](https://s1.ax1x.com/2022/09/07/vbFxJA.png)

![](https://s1.ax1x.com/2022/09/07/vbFbqO.png)

经过这一系列操作以后，我们会得到一串代码，在这里：<http://livere.com/insight/myCode>：

![](https://s1.ax1x.com/2022/09/07/vbFvid.png)

复制`data-uid`里的内容，然后找到如下配置：

![](https://s1.ax1x.com/2022/09/07/vbFXIH.png)

直接把你的`data-uid`复制进去就好了。看一下渲染的效果：

![](https://s1.ax1x.com/2022/09/07/vbFOde.png)

#### 5.5.2 `GiTalk`

`GiTalk`的话是一个很“程序员”的评论系统。基于`GitHub`，支持`Markdown`，简单而优雅。不过，除了一些基本的配置以外，我们还需要更换`CORS Anywhere`的代理。我们先找到它的配置，看一下需要些什么：

![](https://s1.ax1x.com/2022/09/10/vLjhLQ.png)

```yml
# Gitalk
# For more information: https://gitalk.github.io, https://github.com/gitalk/gitalk
gitalk:
  enable: false
  github_id: # GitHub repo owner
  repo: # Repository name to store issues
  client_id: # GitHub Application Client ID
  client_secret: # GitHub Application Client Secret
  admin_user: # GitHub repo owner and collaborators, only these guys can initialize gitHub issues
  distraction_free_mode: true # Facebook-like distraction free mode
  # Gitalk's display language depends on user's browser or system environment
  # If you want everyone visiting your site to see a uniform language, you can set a force language value
  # Available values: en | es-ES | fr | ru | zh-CN | zh-TW
  language: 
```

另外，这是人家的官网：

![](https://s1.ax1x.com/2022/09/10/vLjWQS.png)

##### 5.5.2.1 获取`GitHub Application`

大部分配置都好填，可是这个`client_id`和`client_secret`怎么办？我们需要自己新建一个`GH App`。打开<https://github.com/settings/developers>，并新建一个`Oauth APP`（右上角的按钮）：

![](https://s1.ax1x.com/2022/09/10/vLj2z8.png)

之后需要输入应用名称，应用官网（`Homepage URL`和`Authorization callback URL`），这两个一定一定要一样的，并且得加上`https://`。

![](https://s1.ax1x.com/2022/09/10/vLjfsg.png)

注册以后复制`Client ID`，新建`Client secret`，按红框里的按钮。

![](https://s1.ax1x.com/2022/09/10/vLjgRf.png)

新建后务必立刻复制，否则就只能重新建了。

![](https://s1.ax1x.com/2022/09/10/vLj5Zj.png)

然后我们写到配置的`client_id`和`client_secret`里即可。至于其他的配置的话：

```yml
# Gitalk
# For more information: https://gitalk.github.io, https://github.com/gitalk/gitalk
gitalk:
  enable: false
  github_id: # GitHub repo owner
  repo: # Repository name to store issues
  client_id: # GitHub Application Client ID
  client_secret: # GitHub Application Client Secret
  admin_user: # GitHub repo owner and collaborators, only these guys can initialize gitHub issues
  distraction_free_mode: true # Facebook-like distraction free mode
  # Gitalk's display language depends on user's browser or system environment
  # If you want everyone visiting your site to see a uniform language, you can set a force language value
  # Available values: en | es-ES | fr | ru | zh-CN | zh-TW
  language:
```

`enable`打开，`github_id`写上你的`GitHub`用户名，`repo`是你网站的仓库名（比如`guleixibian2009.github.io`），`admin_user`还是填自己的用户名。`distraction_free_mode`和`language`自己按喜好调即可。

##### 5.5.2.2 配置`proxy`

设置是好了，可是在用之前我们还需要改`CORS Anywhere`的镜像。我们如何把`proxy`改掉呢？参阅`GiTalk`的`README`（见“致谢”，6），有一个`proxy`的选项。

我们找一下这个文件（`themes/next/layout/_third-party/comments/gitalk.swig`）：

![](https://s1.ax1x.com/2022/09/10/vOEatO.png)

有这样一段代码。然后，把下面这段代码复制到里面去，如下：

```js
proxy       : 'https://proxy.cors.sh/https://github.com/login/oauth/access_token'
```

最后的效果就是：

```js
NexT.utils.loadComments(document.querySelector('#gitalk-container'), () => {
  NexT.utils.getScript('{{ gitalk_js_uri }}', () => {
    var gitalk = new Gitalk({
      clientID    : '{{ theme.gitalk.client_id }}',
      clientSecret: '{{ theme.gitalk.client_secret }}',
      repo        : '{{ theme.gitalk.repo }}',
      owner       : '{{ theme.gitalk.github_id }}',
      admin       : ['{{ theme.gitalk.admin_user }}'],
      id          : '{{ gitalk_md5(page.path) }}',
      {%- if theme.gitalk.language == '' %}
        language: window.navigator.language || window.navigator.userLanguage,
      {% else %}
        language: '{{ theme.gitalk.language }}',
      {%- endif %}
      distractionFreeMode: {{ theme.gitalk.distraction_free_mode }},
      proxy       : 'https://proxy.cors.sh/https://github.com/login/oauth/access_token'
    });
    gitalk.render('gitalk-container');
  }, window.Gitalk);
});
```

如果没看出来区别的话就直接复制替换即可。然后我们重新渲染，试一下：

![](https://s1.ax1x.com/2022/09/10/vOEY0x.png)

不过如果需要尝试登录的话一定要部署之后才能测试...所以上线试一下登录：

![](https://s1.ax1x.com/2022/09/10/vOEt76.png)

然后`GiTalk`会自动创建一个`Issue`。我们应该可以在仓库里找到这样一个`Issue`，标题就是文章名：

![](https://s1.ax1x.com/2022/09/10/vOEUAK.png)

如果一切正常的话，我们就配置成功了！

### 5.6 鼠标点击特效

当你点击页面时，你（之前是）可以看到一个彩色的爱心（的）。这个的话，先复制下面的代码：

```js
!function(e,t,a){function n(){c(".heart{width: 10px;height: 10px;position: fixed;background: #f00;transform: rotate(45deg);-webkit-transform: rotate(45deg);-moz-transform: rotate(45deg);}.heart:after,.heart:before{content: '';width: inherit;height: inherit;background: inherit;border-radius: 50%;-webkit-border-radius: 50%;-moz-border-radius: 50%;position: fixed;}.heart:after{top: -5px;}.heart:before{left: -5px;}"),o(),r()}function r(){for(var e=0;e<d.length;e++)d[e].alpha<=0?(t.body.removeChild(d[e].el),d.splice(e,1)):(d[e].y--,d[e].scale+=.004,d[e].alpha-=.013,d[e].el.style.cssText="left:"+d[e].x+"px;top:"+d[e].y+"px;opacity:"+d[e].alpha+";transform:scale("+d[e].scale+","+d[e].scale+") rotate(45deg);background:"+d[e].color+";z-index:99999");requestAnimationFrame(r)}function o(){var t="function"==typeof e.onclick&&e.onclick;e.onclick=function(e){t&&t(),i(e)}}function i(e){var a=t.createElement("div");a.className="heart",d.push({el:a,x:e.clientX-5,y:e.clientY-5,scale:1,alpha:1,color:s()}),t.body.appendChild(a)}function c(e){var a=t.createElement("style");a.type="text/css";try{a.appendChild(t.createTextNode(e))}catch(t){a.styleSheet.cssText=e}t.getElementsByTagName("head")[0].appendChild(a)}function s(){return"rgb("+~~(255*Math.random())+","+~~(255*Math.random())+","+~~(255*Math.random())+")"}var d=[];e.requestAnimationFrame=function(){return e.requestAnimationFrame||e.webkitRequestAnimationFrame||e.mozRequestAnimationFrame||e.oRequestAnimationFrame||e.msRequestAnimationFrame||function(e){setTimeout(e,1e3/60)}}(),n()}(window,document);
```

然后在`themes/next/source/js/src`这个文件夹（自己创建）中，新建`clicklove.js`，代码复制进去即可。我们有了代码，但如何引用呢？我们需要找到模板文件（`themes/next/layout/_layout.swig`），并复制如下代码到这个位置：

```html
<!-- 页面点击小红心 -->
<script type="text/javascript" src="js/src/clicklove.js"></script>
```

粘贴到这里：

```html
  ...

  {%- if theme.pjax %}
    <div id="pjax">
  {%- endif %}
  {% include '_third-party/math/index.swig' %}
  {% include '_third-party/quicklink.swig' %}

  {{- next_inject('bodyEnd') }}
  {%- if theme.pjax %}
    </div>
  {%- endif %}

  <!-- 页面点击小红心 -->
  <script type="text/javascript" src="js/src/clicklove.js"></script>
</body>
</html>
```

然后重新渲染试试：

![](https://s1.ax1x.com/2022/09/11/vOyFds.png)

然后现在我用的烟花的话，原理类似，新建一个`fireworks.js`，里面复制：

```js
class Circle {
  constructor({ origin, speed, color, angle, context }) {
    this.origin = origin
    this.position = { ...this.origin }
    this.color = color
    this.speed = speed
    this.angle = angle
    this.context = context
    this.renderCount = 0
  }

  draw() {
    this.context.fillStyle = this.color
    this.context.beginPath()
    this.context.arc(this.position.x, this.position.y, 2, 0, Math.PI * 2)
    this.context.fill()
  }

  move() {
    this.position.x = (Math.sin(this.angle) * this.speed) + this.position.x
    this.position.y = (Math.cos(this.angle) * this.speed) + this.position.y + (this.renderCount * 0.3)
    this.renderCount++
  }
}

class Boom {
  constructor ({ origin, context, circleCount = 16, area }) {
    this.origin = origin
    this.context = context
    this.circleCount = circleCount
    this.area = area
    this.stop = false
    this.circles = []
  }

  randomArray(range) {
    const length = range.length
    const randomIndex = Math.floor(length * Math.random())
    return range[randomIndex]
  }

  randomColor() {
    const range = ['8', '9', 'A', 'B', 'C', 'D', 'E', 'F']
    return '#' + this.randomArray(range) + this.randomArray(range) + this.randomArray(range) + this.randomArray(range) + this.randomArray(range) + this.randomArray(range)
  }

  randomRange(start, end) {
    return (end - start) * Math.random() + start
  }

  init() {
    for(let i = 0; i < this.circleCount; i++) {
      const circle = new Circle({
        context: this.context,
        origin: this.origin,
        color: this.randomColor(),
        angle: this.randomRange(Math.PI - 1, Math.PI + 1),
        speed: this.randomRange(1, 6)
      })
      this.circles.push(circle)
    }
  }

  move() {
    this.circles.forEach((circle, index) => {
      if (circle.position.x > this.area.width || circle.position.y > this.area.height) {
        return this.circles.splice(index, 1)
      }
      circle.move()
    })
    if (this.circles.length == 0) {
      this.stop = true
    }
  }

  draw() {
    this.circles.forEach(circle => circle.draw())
  }
}

class CursorSpecialEffects {
  constructor() {
    this.computerCanvas = document.createElement('canvas')
    this.renderCanvas = document.createElement('canvas')

    this.computerContext = this.computerCanvas.getContext('2d')
    this.renderContext = this.renderCanvas.getContext('2d')

    this.globalWidth = window.innerWidth
    this.globalHeight = window.innerHeight

    this.booms = []
    this.running = false
  }

  handleMouseDown(e) {
    const boom = new Boom({
      origin: { x: e.clientX, y: e.clientY },
      context: this.computerContext,
      area: {
        width: this.globalWidth,
        height: this.globalHeight
      }
    })
    boom.init()
    this.booms.push(boom)
    this.running || this.run()
  }

  handlePageHide() {
    this.booms = []
    this.running = false
  }

  init() {
    const style = this.renderCanvas.style
    style.position = 'fixed'
    style.top = style.left = 0
    style.zIndex = '999999999999999999999999999999999999999999'
    style.pointerEvents = 'none'

    style.width = this.renderCanvas.width = this.computerCanvas.width = this.globalWidth
    style.height = this.renderCanvas.height = this.computerCanvas.height = this.globalHeight

    document.body.append(this.renderCanvas)

    window.addEventListener('mousedown', this.handleMouseDown.bind(this))
    window.addEventListener('pagehide', this.handlePageHide.bind(this))
  }

  run() {
    this.running = true
    if (this.booms.length == 0) {
      return this.running = false
    }

    requestAnimationFrame(this.run.bind(this))

    this.computerContext.clearRect(0, 0, this.globalWidth, this.globalHeight)
    this.renderContext.clearRect(0, 0, this.globalWidth, this.globalHeight)

    this.booms.forEach((boom, index) => {
      if (boom.stop) {
        return this.booms.splice(index, 1)
      }
      boom.move()
      boom.draw()
    })
    this.renderContext.drawImage(this.computerCanvas, 0, 0, this.globalWidth, this.globalHeight)
  }
}

const cursorSpecialEffects = new CursorSpecialEffects()
cursorSpecialEffects.init()
```

然后把`_layout.swig`里改一下就好了。效果的话，点击一下试试？

### 5.7 把猫...养在博客？

这一步也是很简单的啊。对对，我说的就是左下角那只白猫......

![](https://s1.ax1x.com/2022/09/11/vO5tUS.png)

这个插件叫做`live2d`。官方地址的话，<https://github.com/xiazeyu/live2d-widget-models/>可以查到所有的`model`。这只猫的话，它叫`tororo`，虽然我也不知道为啥...我们需要先安装依赖：

```powershell
npm install hexo-helper-live2d live2d-widget-model-tororo
```

但这样还不太行。我们需要加一段配置，加在`Hexo`的`_config.yml`里：

```yml
# live2d performance
live2d:
  enable: true
  scriptFrom: local
  pluginRootPath: live2dw/
  pluginJsPath: lib/
  pluginModelPath: assets/
  tagMode: false
  debug: false
  model:
    use: live2d-widget-model-tororo
  display:
    position: left
    width: 280
    height: 560
  mobile:
    show: true
```

我并没有了解过所有的参数，反正就是把`use`改成`live2d-widget-model-tororo`，同时改一下位置、长、宽即可。

嘿嘿，看起来这一段很短，对吧？其实我当时研究了很久，网上没有太好的教程，最后才发现要安装`hexo-helper-live2d`啊。

### 5.8 `AddThis Utilities`分享功能

虽然我这个博客还是没什么名气，可万一之后需要有一个分享功能，怎么办？在`Next`的配置中提到了`Addthis`分享。这个怎么实现呢？

![](https://s1.ax1x.com/2022/09/11/vO7Ca6.png)

先到`addthis.com`注册一个账号（另及：加速`Google Recaptcha`的方法见之后的文章），然后照着这些截图来：

登录之后有这样一个页面，我们选择第一个，`Share Buttons`；

![](https://s1.ax1x.com/2022/09/11/vO79Vx.png)

然后，选择`Floating`；

![](https://s1.ax1x.com/2022/09/11/vO7Sq1.png)

之后我们开始自定义工具。先选择`Selected by you`，用`ADD MORE SERVICES`改分享方式；

![](https://s1.ax1x.com/2022/09/11/vOTzrR.png)

最后我选了这些，比如微信、QQ、生成二维码等等；

![](https://s1.ax1x.com/2022/09/11/vO7PIK.png)

在第四个栏目里调整一下位置，和手机是否显示；

![](https://s1.ax1x.com/2022/09/11/vO7kGD.png)

最后`Activate Tool`，获取代码；

![](https://s1.ax1x.com/2022/09/11/vO7ARe.png)

不过我们不需要所有的代码，找一下代码里的`pubid`，应该是`ra-`打头，接着复制进配置文件里即可。

![](https://s1.ax1x.com/2022/09/11/vO7FPO.png)

渲染看一下。

> 另及：如果没有的话，检查一下是否浏览器屏蔽了“跟踪器”。

> 还有...我本来想继续写下去，写一个`Widgetpack`打分功能。可惜人家服务器有问题，功能暂时下线了，等恢复了我再加上吧。

好耶！我们现在就把这8个功能配置完啦！接下来...我们来看一点更高级的东东！

---

## 6. 更高级的功能

这一章的话，主要讲一些“看不见”的东西，比如站点地图，`RSS`等等。

### 6.1 `RSS`订阅

一般博客都是提供`RSS Feed`来订阅的。之前我们提到过`RSS`，包括侧边栏链接、文章结尾的友链，等等。要生成的话我们只需要安装插件`hexo-generator-feed`，每次`hexo g`都会自动生成。

```powershell
npm install hexo-generator-feed --save
```

不过，生成出来的文件在哪里呢？看一下...应该是`/atom.xml`。

![](https://s1.ax1x.com/2022/09/11/vXpMo4.png)

### 6.2 站点地图`sitemap`

站点地图的话主要是为搜索引擎用的，这一小节算是给后文的一个铺垫。同样的，只需要安装插件`hexo-generator-sitemap`即可。这次生成出来的是`/sitemap.xml`。

![](https://s1.ax1x.com/2022/09/11/vXpueU.png)

### 6.3 `CDN`与图床

默认的话，`next`会使用`jsdelivr`作为默认的`CDN`，不过`cdn.jsdelivr.net`这个节点不是特别的稳定（被墙过），所以我个人是换到了`fastly`节点上。具体位置的话，在这里，至于改不改就看你自己了。

![](https://s1.ax1x.com/2022/09/11/vXplFJ.png)

同时如果你想要往文章里添加图片，那光靠自己的域名（也就是`GitHub`）肯定是不够的，我们一定会需要一个快速的、稳定的图床。我个人推荐是`imgse`路过图床，它这个是免费的，而且已经有10年历史，上传也非常方便。它支持`10MB`内的`JPG`和`PNG`，子节点是`ax1x.com`。

![](https://s1.ax1x.com/2022/09/12/vXoGPU.png)

### 6.4 `Bing SEO`

搜索引擎优化确实是一件很重要的事情，最简单的是`Bing`。官网的话，<https://www.bing.com/webmasters/about/>，用`Microsoft`账户登录是最方便的（除非你有`FB`或者`Google`，不过这不太可能吧）。

![](https://s1.ax1x.com/2022/09/11/vXpKwF.png)

![](https://s1.ax1x.com/2022/09/11/vXpmLT.png)

#### 6.4.1 注册与验证

登录进来之后，我们输入网址，登记页面（页面布局可能和图片有些许区别）。

![](https://s1.ax1x.com/2022/09/11/vXpJQx.png)

登记过后会要求我们验证页面。三种方法中最简单的是`<meta>`标签，直接复制代码，然后加到`_layout.swig`的`<head>`里去就好了。重新渲染、部署，然后等待片刻、验证。

![](https://s1.ax1x.com/2022/09/11/vXpGS1.png)

![](https://s1.ax1x.com/2022/09/11/vXpYy6.png)

![](https://s1.ax1x.com/2022/09/11/vXp3WR.png)

这就代表验证成功了。

#### 6.4.2 提交网站地图

点击右上角那个“提交站点地图”，并输入你刚生成的站点地图的网址，可以加速爬网。

![](https://s1.ax1x.com/2022/09/11/vXp1Y9.png)

![](https://s1.ax1x.com/2022/09/11/vXptOK.png)

然后...等待扫描...可能会需要一段时间。

这就代表扫描完了：

![](https://s1.ax1x.com/2022/09/11/vX9CX6.png)

不过真正能搜到是需要2天时间的，先放一下我自己的博客的截图：

![](https://s1.ax1x.com/2022/09/11/vX9inK.png)

当然这个`SEO`肯定是不止这么多的。相关的功能等着你去探索，包括`Microsoft Clarity`等等。

### 6.5 模板文件与动态样式表

最后这一小节不是具体的教你去“干什么”，而是具体“怎么干”。每个人对网站的外观跟行为逻辑有自己的看法，而自定义的终极方式就是修改底层。

![](https://s1.ax1x.com/2022/09/24/xAMc4I.png)

在`Next`这个主题下，关于底层的两个文件夹，一个是`layout`，一个是`source`，具体见下：

#### 6.5.1 `Mozilla Nunjucks`

在上网查之前我一直以为我们修改的什么`_layout.swig`啊都是用什么`swig`语言写的，但一搜其实并没有这个语言（有，但极其小众，且已为`unmaintained`状态）。直到我看到`renderer.js`里的代码：

```js
/* global hexo */

'use strict';

const nunjucks = require('nunjucks');
const path = require('path');

...

// Return a compiled renderer.
njkRenderer.compile = function(data) {
  const compiledTemplate = njkCompile(data);
  // Need a closure to keep the compiled template.
  return function(locals) {
    return compiledTemplate.render(locals);
  };
};

hexo.extend.renderer.register('njk', 'html', njkRenderer);
hexo.extend.renderer.register('swig', 'html', njkRenderer);
```

才发现有`nunjucks`这种语言。它的语法可以在官网<https://mozilla.github.io/nunjucks/>查到，据说和`jinja2`（基于`Python`的）一模一样，此外还支持自定义后缀什么的。这里讲一点特殊的变量，举些例子：

```jinja2
{%- if theme.pjax %}
    <div id="pjax">
  {%- endif %}
  {% include '_third-party/math/index.swig' %}
  {% include '_third-party/quicklink.swig' %}

  {{- next_inject('bodyEnd') }}
  {%- if theme.pjax %}
    </div>
  {%- endif %}
```

（来自`_layout.swig`）有一个`if`语句，后面跟的是`theme.pjax`。这个`theme`指的是`Next`主题的`_config.yml`。

```jinja2
<div class="site-author motion-element" itemprop="author" itemscope itemtype="http://schema.org/Person">
  {%- if theme.avatar.url %}
    <img class="site-author-image" itemprop="image" alt="{{ author }}"
      src="{{ url_for(theme.avatar.url) }}">
  {%- endif %}
  <p class="site-author-name" itemprop="name">{{ author }}</p>
  <div class="site-description" itemprop="description">{{ description }}</div>
</div>
```

（来自`_partials/sidebar/site-overview.swig`）这里引用了一个变量`{{ author }}`，像这种没有`theme.`的都来自`Hexo`的`_config.yml`。

```jinja2
{% block title %}{{ page.title }} | {{ title }}{% endblock %}
```

（来自`post.swig`）这里引用的`{{ page.title }}`有前缀`page.`，代表当前正渲染的页面（准确地说是`post`或`page`的`Front Matter`）。

#### 6.5.2 `Stylus`

这个就没太多好讲的了，因为我自己也没学过动态`CSS`。在`source/css`这个文件夹下所有`.styl`后缀的文件都是样式表。我们之前修改过一个书签的，还记得吗？

---

## 7. 总结与回顾

到这里，我们所有的教程已经写完了。在这“短暂的”几十分钟，几小时，甚至几天中，我们终于成功的做出来这样一个基于`Hexo`+`Next`的博客网站了。还记得那几条命令吧，我还是写在这里备用。

- `hexo clean`清除本地缓存

- `hexo g`生成网页

- `hexo s`打开本地服务器

- `hexo d`部署到远程

- `hexo new`新建文章

- `hexo new page`新建页面

接下来，就是你继续探索，大展身手的时刻了！嗯...48k字，我也是圆了长久以来的梦想。那么，我们就下次再见喽\~

---

## 8. 致谢

这里写一下我参考到的文章：

1. [基于Github.io+Hexo搭建个人博客 | JerryMiao2019's Blog](https://jerrymiao2019.github.io/2021/04/10/%E5%9F%BA%E4%BA%8EGithub-io-Hexo%E6%90%AD%E5%BB%BA%E4%B8%AA%E4%BA%BA%E5%8D%9A%E5%AE%A2/)

2. [解决hexo-renderer-kramed渲染冲突的部分问题 | 卡洛的核心舱](https://corecabin.cn/2021/08/14/solve-some-problems-of-hexo-renderer-kramed-rendering-conflicts/)

3. [Hexo+Next主题优化 | 知乎](https://zhuanlan.zhihu.com/p/30836436)

4. [Hexo博客优化之Next主题美化 | nightmare_dimple的博客 | CSDN博客](https://blog.csdn.net/nightmare_dimple/article/details/86661502)

5. [Hexo 常见问题解决方案 | Anran758's blog](https://anran758.github.io/blog/2020/09/27/hexo-issue/)

6. [GitHub - gitalk/gitalk](https://github.com/gitalk/gitalk#options)

7. [Hexo给NexT主题内添加页面点击出现爱心的效果_| 女王的禅师范的博客 | CSDN博客](https://blog.csdn.net/qq_34146679/article/details/86065071)

8. [Hexo-NexT 添加打字特效、鼠标点击特效 | 小丁的个人博客](https://tding.top/archives/58cff12b.html)

9. [Hexo+yilia添加helper-live2d插件宠物动画，很好玩的哦~~ | 王约翰 | 博客园](https://www.cnblogs.com/wangyuehan/p/9860371.html)

10. [Github 搭建 hexo （五）- 站点地图（sitemap.xml）|_Small蒙奇的博客 | CSDN博客](https://blog.csdn.net/u010053344/article/details/50706790)

**THE END**感谢您的阅读\~
