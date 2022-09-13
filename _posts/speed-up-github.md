---
title: 3个小妙招加速你的GitHub~
date: 2021-08-14 08:10:08
tags:
- Github
- DevSidecar
- FAQs
categories:
- GitHub
- [加速, GitHub]
---

想必大家都知道`Github`是一个极佳的云端代码储存、交流平台，同时你也可以简单粗暴地把它当作云盘或者服务器。
但在众多优点之中，有一个问题却一直深深地困扰着我，那就是`GitHub`实在太！慢！啦！  

<!-- more -->

在我头几次用Github的时候，我几乎根本上不去，不过以前不过是下载一些搜索到的小工具啥的。
但现在不一样了。我开始做网站，开始天天*（也许不是天天）*更新，每一次都等待几十分钟的加载时间（白天还好），简直就是浪费生命。相信大家都有同感吧！  
于是，我就整理了下面3种方法，给大家节约“生命”。

## 0. 目录

- 方法一：修改`Host`，其实更加浪费生命  
- 方法二：改链接，做镜像，世界变得更加美好  
- 方法三：装“边车”，速度嗖嗖嗖直窜3秒！  

___

## 1. 我有大把时间，我要改`hosts`！

好吧，如果你真的这么无聊，那我就讲一讲吧......  
首先在`C:\Windows\System32\drivers\etc`找到`hosts`文件。如果你以前没用过，那可能需要打开权限。（如下图）

![hosts1](https://z3.ax1x.com/2021/08/15/fcKoNV.png)

![hosts2](https://z3.ax1x.com/2021/08/15/fcKLjJ.png)

![hosts3](https://z3.ax1x.com/2021/08/15/fcKXu9.png)

用记事本打开，这个文件里在没有改动的情况下只有几行注释，忽略即可。  
现在我们到 [`Ipaddress`](https://www.ipaddress.com) 或者[`itdog`](https://www.itdog.cn/ping/)查下面三个网址的`IP`，现在（其实是很久很久以前）查询如下：

| 网址                              | 解释   | IP               |
|:-------------------------------:|:----:|:----------------:|
| `github.com`                    | 这是主站 | ~~140.82.114.4~~ |
| `raw.githubusercontent.com`     | 动态资源 | 185.199.108.153  |
| `raw.githubusercontent.com`     | 动态资源 | 185.199.109.153  |
| `raw.githubusercontent.com`     | 动态资源 | 185.199.110.153  |
| `raw.githubusercontent.com`     | 动态资源 | 185.199.111.153  |
| `avatars.githubusercontent.com` | 你的头像 | 185.199.108.133  |
| `avatars.githubusercontent.com` | 你的头像 | 185.199.109.133  |
| `avatars.githubusercontent.com` | 你的头像 | 185.199.110.133  |
| `avatars.githubusercontent.com` | 你的头像 | 185.199.111.133  |

注意，写入`hosts`的格式如下：

```hosts
IPAddress HostName
```

如：

```hosts
140.82.114.4    github.com  
185.199.108.153 raw.githubusercontent.com  
185.199.109.153 raw.githubusercontent.com  
185.199.110.153 raw.githubusercontent.com  
185.199.111.153 raw.githubusercontent.com
185.199.108.133 avatars.githubusercontent.com
185.199.109.133 avatars.githubusercontent.com
185.199.110.133 avatars.githubusercontent.com
185.199.111.133 avatars.githubusercontent.com
```

按照这样的格式输入到 `hosts` 文件里，再访问 `Github` 应该就很快了！  
**小提示：每次只用查主站的`IP`就好了，其他的基本不会变\~你可以在`itdog`中选择一些类似镜像的`IP`，比如`20.205.243.166`等等。**

___

## 2. 我只用`GitHub`下载程序，不使用其他功能！

### 2.1 `Git`版

如果你是用`Git Clone`仓库，那么你就走运了。平时，我们`Clone`时语法是这样的：

```git
git clone https://github.com/guleixibian2009/guleixibian2009.github.io.git
```

但如果你用了镜像网站，速度会极快：

```git
git clone https://hub.nuaa.cf/guleixibian2009/guleixibian2009.github.io.git
```

`https://hub.nuaa.cf`是一个极为神奇的网站：作为一个镜像网站，他把几`KiB/S`的速度提到了几百`MiB/S`，速度大幅提升！  
但这样会有一个`bug`：`Git`会把你`Push`回去的网址变`https://hub.nuaa.cf`。很尴尬的是，这并不是你想要`Push`回去的地址，于是，经过无数尝试，我发现在`.git`文件夹（是隐藏的）中有一个`config`文件，里边是这样写的：

```
......

[remote "origin"]
    url = https://hub.nuaa.cf/guleixibian2009/guleixibian2009.github.io.git
    fetch = +refs/heads/*:refs/remotes/origin/*

......
```

有没有注意到那个`url`后面跟了一个`https://hub.nuaa.cf`？
为了让它“恢复正常”，要把它改回`https://github.com`。  
现在，应该就可以了吧！_（如果没有`.git`文件夹说明你没有`Push`过，或者这不是你的项目）_

### 2.2 网页版

`https://hub.nuaa.cf`并不是`GitHub`的唯一镜像。如果你觉得`GitHub`太慢，
你可以注册一个中文版`GitHub`，叫做`Gitee`。  
注册后，点击`+`号，并且导入你的`GitHub`仓库，继续下载就超级快乐啦！
![import1](https://z3.ax1x.com/2021/08/15/fcKjBR.png)
![import2](https://z3.ax1x.com/2021/08/15/fcKvH1.png)

___

## 3. 我天天要用`GitHub`，给个靠谱的方法！

在`GitHub`上有一个项目，叫做`@docmirror/DevSidecar`，中文名叫`开发者边车`（也就是我现在用的）。  
**_小提示：使用此系统可能会造成系统代理服务器配置更变，请小心驾驶_**  
这个软件是我某个同学推荐的，几乎解决了关于`Github`速度的所有问题。（后来，22年6月它又帮我解决一个大难题，众所周知`jsdeilvr`这时被墙了……）
如果你需要下载或帮助，请去他的 [`Github`项目地址](https://github.com/docmirror/dev-sidecar)（这个项目在`gitee`上面已经被封锁了）。
用之前要先按指导安装证书，随后选择默认模式。

![sidecar1](https://z3.ax1x.com/2021/08/15/fcMSN6.png)
![sidecar2](https://z3.ax1x.com/2021/08/15/fcMp4K.png)

不过后来我又发现一个问题......如果你用的是`Firefox`，那么他有时会有“未连接”的界面。

![problem](https://z3.ax1x.com/2021/08/15/fcKzAx.png)  

白天速度不算慢，你就关掉代理就好了。不过如果你无法忍受的话，你可以把边车调成安全模式，这个模式不需要证书。实际上，造成刚刚那个界面的原因就是`Firefox`无法识别边车自动生成的证书。  
所以，你学废了吗？  
不过，经过一“晚上”的查询，我终于查到了一个解决办法。  
在网址栏里输入`about:config`，会显示如下界面，我们可以通过修改底层配置的方法来解决这个问题。

![config1](https://z3.ax1x.com/2021/08/15/fcKH9U.png)

点击“接受风险并继续”，会显示如下界面，我们输入`security.enterprise_roots.enabled`。

![config2](https://z3.ax1x.com/2021/08/15/fcKThT.png)

我们默默地把布尔值修改成`True`，重启浏览器，搞定！

![config3](https://z3.ax1x.com/2021/08/15/fcKqc4.png)

如果点击“那把锁”后出现如下界面，说明你成功啦！

___

现在你有没有发现自己空出来了大把时间呢？借助这三种方法，好好“享受”你的编程时光吧！

__THE END__ 谢谢你的阅读~
