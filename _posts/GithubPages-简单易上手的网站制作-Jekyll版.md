---
title: GithubPages-简单易上手的网站制作(Jekyll版)
date: 2021-08-15 20:29:48
tags:
- Github
- Website
- Jekyll
categories:
- GitHub
- [ GitHub,Pages ]
---

其实我一直想要做网站。在6个月前（2021年2月），我开始看着 [`W3School`](https://www.w3school.com.cn/)上的教程，用`SublimeText`写`HTML`。
但写了一两个月后，我突然想起来一件事。大概在一年前，我有个同学给我推荐了一个录屏软件（不过我忘了叫什么了，好像是`Captura`？）。他给了我一个网址，然后，__我看到了一个熟悉的东西__————这个网址里有_`Github`_的字样。于是，我搜（百）索（度）了一会子，然后搜到好多有关“用_`Github.io`_创作个人博客”的文章，点开后没想到做网站也可以这么简单。今天我来教大家创建一个`GithubPages(github.io)`页面，分享一下我做网站时的心得。

<!--more-->

## 0. 步骤分解

__话不多说，直接上步骤！__    
1.注册github，创建`<username>.github.io`仓库；  
2.创建`index.md`；  
3.修改`_config.yml`，选择样式；  
4.404页面；

___

## 1. 基础设置

看完上文，大家已经知道了我们的网站依托于 [`GitHub`](https://github.com/) 的 __[`Pages`](https://pages.github.com/)__ 功能。
身为程序员，大家肯定都听说过`GitHub`吧。如果你还不知道的话，可以查询 [百度百科](https://baike.baidu.com/item/Github) 。

### 1.1 注册`GitHub`账号

（如果你有`GitHub`账号，请跳过这一步）如果你没用过`GitHub`，就去官网注册一个账号，步骤如下：  
如图，填写你的邮箱和用户名，应该就好了。会有一系列验证，比如说生日和性别等。

![frontpage](https://z3.ax1x.com/2021/08/15/fgxQoR.png)
![email](https://z3.ax1x.com/2021/08/15/fgxKeJ.png)

（尴尬：我注册时不是这样啊？？？）  
登录`GitHub`可能会需要验证码。登录一下注册时的邮箱，你会收到`GitHub`（`noreply@github.com`）的邮件，比如说：

![Authentication](https://z3.ax1x.com/2021/08/15/fgxeQU.png)

### 1.2 创建一个仓库

为了储存我们的代码，我们需要分配给他一个空间，学名 `repository` ，意思是仓库。  
如图，点击右上角的 `New` 按钮，然后会弹出如下界面。

![create1](https://z3.ax1x.com/2021/08/15/fgxkiq.png)
![create2](https://z3.ax1x.com/2021/08/15/fgxmyF.png)

我们如图勾选，

![create3](https://z3.ax1x.com/2021/08/15/fgxnL4.png)

在 `<username>` 处填上你的名字，如果名字是 `EdogawaNotFound` , 那仓库名就叫  
`edogawanotfound.github.io`。如果是我的话，我也许会设成`guleixibian2009.github.io`。 

现在你应该有了一个新仓库了。有了自己的仓库，就可以往仓库里放东西了。

___

## 2. 切入正题

### 2.1 勾选`Pages`

在使用这个功能之前，你要告诉`GitHub`你要把这个仓库当做网页源码。  
在 `Settings` 里找到 `pages` 选项，应该是这样子的：

![settings2](https://z3.ax1x.com/2021/08/15/fgxwTA.png)

把 `Source` 调成你现有的分支，点击 `Save` 。  

![settings3](https://z3.ax1x.com/2021/08/15/fgxBFI.png)

### 2.2 新建`index.md`

![change1](https://z3.ax1x.com/2021/08/15/fgxEWV.png)

为了`Github Pages`更好的识别你的主页，我们需要新建一个`index.md`。你可以保留你的`README`不动，没有关系。

![New1](https://z3.ax1x.com/2021/08/15/fgxtyD.png)

点击 `+` 按钮，选择`Create New File`，然后进入如下界面：

![New2](https://z3.ax1x.com/2021/08/15/fgxdwd.png)

在输入框里输入`index.md`。`Index`指索引。你将会在这个新文件里写主页。

![New3](https://z3.ax1x.com/2021/08/15/fgxNOe.png)

点击`Commit New Changes`。  
你的网站，如果已经`Publish`，应该叫做`<username>.github.io`。现在访问你的网站，如果可以访问，恭喜你，你已经成功了！   
但是一个网站只有主页实在无聊，所以，为了让你的网站看起来更加高级亿点点，我们就要开始写文章了。
使用`GitHub Pages`功能时，你并不需要会写`HTML`，只需要写文章就行了。 而在`Github Pages`功能里，我们写文章的方法是写`Markdown`。  
等等，为什么我觉得我的界面太难看了呢？？？(￣ε(#￣)☆╰╮(￣▽￣///))让我们给自己的网站换个样式。  
不过，如果你想现在学习`Markdown`了。我另写了一篇文章， [传送门](https://guleixibian2009.github.io/2021/08/25/Markdown基本语法/) 。  

### 2.3 换个样式

一个网站，也许最重要的不是文章的内容，而是它的门面，而一个“光鲜靓丽”的主页则是一个很好的选择。  
`GithubPages`已经给你提供好了一些样式，我们可以直接用。  
转到刚刚那个`Settings/Pages`,不过这次点`ThemeChooser`。

![settings3](https://z3.ax1x.com/2021/08/15/fgxBFI.png)

在这个界面，你可以选择一个你喜欢的样式（`Theme`）。

![theme1](https://z3.ax1x.com/2021/08/15/fgxDYt.png)

在这里面我选了一个`Cayman`（简约大气）。

![theme2](https://z3.ax1x.com/2021/08/15/fgxrfP.png)

不管你选了哪个，有没有发现你的网站好看多了呢？ 
不过，他会自动填充你的`index.md`。网站的默认文本是对`Github Pages`功能的介绍。这样的网站，也许对于别人来说没有意义。
(不过如果没有的话......也许是因为你先创建了文件再选择样式，其实也没事)  

### 2.4 `_config.yml`

不知道细心的你有没有发现，你的仓库里面多了一个`_config.yml`文件（千万不要删！）
打开这个文件，你会发现里面有一行文字：

```yml
theme: jekyll-theme-cayman
```

这个`theme`就指的是样式。`jekyll-theme`指的是`Github Pages`默认给你使用`jekyll`渲染网站界面。  
在这个文件里你可以调整你的网站的标题，仔细看！

![Title](https://z3.ax1x.com/2021/08/15/fgx6l8.png)

其实很简单，只要往下面添加一行就可以啦！

```yml
title: My Website~
```

你，都学废了吗？

___

## 3. `404`页面

在访问你的网站时，别人总有输错网址的时候。`Github`其实有自带的`404`，像这样：

![404](https://z3.ax1x.com/2021/08/15/fgxIf0.png)

不过这个灰色的`404`实在是不好看，那么，我就有了一个疑问：我能不能自己定制一个`404错误`页面呢？答案是肯定的。  

在你的仓库里新建一个`404.md`文件，方法同上。在里面用`Markdown`填充上你想要的内容。比如说，我会这么写（直接上代码）。

```markdowm
# 404 错误
**_你寻找的界面不存在！_**  
即将返回 [主页](https://guleixibian2009.github.io/) ......
```

但实际上，光这么写还是不够。如果你现在访问`https://{username}.github.io/404`，你也许会看到你想要的页面。但如果你访问一个不存在的页面（指你的域名下面的错误网址，自己定义的`404`对其他`github.io`不起作用），它依然会显示那个灰色的`404`。  

所以到底怎么办呢？为了解决这个问题，我们要引入一种新的东西：`YAML Front Matter`。

```yaml
---
permalink: /404.html
---
```

把上面这段代码复制到你的`404.md`的最开头，再次访问应该就有啦！  

---

## 4. 新建页面&文章

现在你已经有了一个主页和`404`页面了。现在，我们将会进入最激动人心的一部分：写博客。

### 4.1 新建博客文件&文件夹

一个网站一般都是“分层”的，其实`Github Pages`也可以做到这一点。如果你想让`Jekyll`在你的仓库中渲染出“子页面”，你可以在仓库中新建一个文件夹。比如说，你可以创建`guleixibian2009.github.io/Github`，这样网址就会被渲染成`https://guleixibian2009.github.io/Github/`。点开新建文件页面，在输入框里输入你想要的页面名，现在你按下`/`，神奇的事情发生了：刚刚输入的名称成功地成为了一个文件夹！然后，继续输入`index.md`，并且`Commit New Changes`，再访问刚刚创建的页面，就可以啦！  

其实，不一定只有一层文件夹。如果你愿意，你可以在一层的基础上再建N个/层文件夹，并在每一个文件夹下建一个`index.md`，就可以啦！现在把你的文章用`Markdown`填进去，再次访问就有新界面啦！

### 4.2 给页面添加特效

虽然我搜了很久，但是我实在没有搜到太多可以直接应用的特效。不过我听说过一种基于`Ruby`的桌面版`Jekyll`，大家可以自行搜索。话说回来，我的确搜到一个特效：404自动跳转回主页。  

其实这个很容易实现，其实是一段`JavaScript`脚本。直接把如下脚本插在`404.md`最底下：

```HTML
<script type="text/javascript"> 
    setTimeout("javascript:location.href='/'", 10000); 
</script>
```

其中，`setTimeout`函数就是定时。而`href='/'`就指的是定时回到根目录。`10000`指10秒。也就是说，10秒钟后返回主页。

---

## 5. `GitHub Pages`的工作原理

说到这大家可能会想，`Pages`能有什么工作原理？

---

## 写在最后

其实利用`Github Pages`作为域名做网站的方法有很多，除了仅仅用网页版`Jekyll`和桌面版`Jekyll`，还有`HEXO`和`Wordpress`等等。大家可以自行去探索，不过，掉了坑我可不救你！🤣

__THE END__ 谢谢你的阅读~
