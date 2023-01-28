---
title: 还需要……加速吗？
date: 2022-09-26 19:29:21
tags:
- Python
- 加速
categories:
- 加速
---

速度，自然是每一个程序员追求的目标。随着本人编程渐渐深入，又发现了一些加速的地方，提高编程效率。这里包含：`pip`镜像、`Microsoft Store`加速、`VSCode`下载链接和`Google Recaptcha`加速。也算是一种小备忘录吧，方便之后，比如重装系统等等。

<!--more-->

## 1. `Python Pip`镜像源

周知所众`Python`官方的包管理器是`Pip`，但很不幸的是`Pypi`官方的源在国内是很慢的，速度大概在`KB`级。我们需要调整它的镜像源，比如国内的阿里云。

![](https://s1.ax1x.com/2022/10/27/xhKN5V.png)

具体的话，先找到`C:/Users`文件夹中你自己的用户文件夹（比如`C:/Users/gulei`），里面新建一个`pip`文件夹。

![](https://s1.ax1x.com/2022/10/27/xhKYEq.png)

在这个文件夹里面新建一个`pip.ini`配置文件，编辑器打开，把如下内容复制进去：

```ini
[global] 
index-url = http://mirrors.aliyun.com/pypi/simple/ 
[install] 
trusted-host = mirrors.aliyun.com
```

这样就可以配置镜像源了。运行一下`pip`，速度就可以供我们正常使用了。

## 2. `Microsoft Store`应用商店临时加速

其实微软的网站和服务速度慢的根本原因在于国内服务商解析不出（大概率是故意的）比较好的`DNS`，这就导致了连接失败的情况，比如`Microsoft Store`总是转圈圈等等。

那怎么办呢？解铃还须系铃人。在不走代理的情况下，最优的解决办法是走微软的`DNS`解析，即`4.4.4.2`或`4.2.2.1`。具体调法，在`IPv4`的属性里面找一下：

![](https://s1.ax1x.com/2022/10/27/xhKtU0.png)

具体来说，就是“网络适配器选项”——某个连接的“属性”——“网络”——“IPv4”，选择手动模式。这样一来，自己家的服务自己家提供，速度就会快很多。不幸的是，微软的`DNS`解析对国内其他网站并不友好，故使用完毕还需调整回“自动”模式，所以我称其为“临时加速”。

## 3. `VS Code`下载`CDN`链接

在编程早期所谓广泛涉猎的时候（或者是暂未决定用哪个专门的编辑器的时候），我会想到`Visual Studio Code`这一款万金油。然而官方的下载链接仍然是对我们不友好的（`KB`级都没有）。但官方`CDN`还是有备用链接的，虽然不公开，但它莫名其妙就是高速。这是原链接：

```
https://az764295.vo.msecnd.net/stable/d045a5eda657f4d7b676dedbfa7aab8207f8a075/VSCodeUserSetup-x64-1.72.2.exe
```

加速的话，只需把`az764295.vo.msecnd.net`换为国内官方镜像`vscode.cdn.azure.cn`即可。

## 4. `Header Editor`与`Google Recaptcha`

转载自一篇文章：[Google 人机验证(reCaptcha)无法显示解决方案(可解决大多数 CSP 问题) &#8211; Azure Zeng Blog](https://blog.azurezeng.com/recaptcha-use-in-china/)

> 前言：为了防止机器人攻击，国外很多网站都使用了 `Google reCaptcha` 验证码。`reCaptcha` 对于国外用户非常的友好，但是… 对于国内用户就不怎么友好了。究其原因，则是国内网络全线屏蔽 `Google` 服务，导致 `reCaptcha `完全加载不出来。这样，国内玩家就无法在对应的网站进行下一步操作了。本方案可以解决 `reCaptcha` 无法加载的问题。

**适用平台**: `Chrome` 电脑版，`Firefox` 电脑版

**适用范围:** **大部分的 `Google` 人机验证的国内加载都可以用这个方案解决。**  
本方案无法修改部分网站的 `Content-Security-Policy`。所以这个方案对于这部分网站是无效的。

请注意，由于方案的特殊性，**少数网络情况下不一定成功**。但是，大部分网络情况下都是可以成功的。

### **第一步 安装插件**

本方案基于 `Header Editor` 插件。因此，您需要先在您的浏览器中安装这个插件。

### 第二步 配置插件

打开 `Header Editor` 插件的配置页面，选择 “导入和导出” 选项。

![](https://i.loli.net/2018/11/03/5bdd57f13c285.png)

此处需要导入我写好的配置。这里提供两种方法（我就直接方法2了）。

方法 2: 导入在线配置

在下载规则中，填入下面的地址 (任选其一，推荐使用 GitHub 版本):

- (GitHub，**推荐**) https://github.azurezeng.com/static/HE-GoogleRedirect.json
- (本站服务器) https://www.azurezeng.com/static/HE-GoogleRedirect.json

*** 重要提醒：建议使用 GitHub 地址。本站服务器地址在站点维护时可能无法使用。**

然后点击下载按钮。

如果先前导入过，你应该可以在下载规则中直接找到这个地址，直接点击旁边的下载按钮即可。

![](https://i.loli.net/2018/11/03/5bdd581a7ef27.png)

接下来你应该会在 “导入” 看到相关规则 (如果之前导入过，“操作” 中的 “添加” 会显示为 “覆盖已有”)。选择 “保存” 即可。

![](https://i.loli.net/2018/11/03/5bdd583f06a1f.png)

最后你的规则列表应该是这样的:

![](https://i.loli.net/2020/07/10/cpxHm8LtME4KGFf.png)

好了，关闭这个页面。然后就可以了，现在 `reCaptcha` 应该可以正常显示了。

原理

这个插件将 `reCaptcha` 的调用 (www.google.com/recaptcha) 直接跳转到了 `reCaptcha` 国内镜像上面 (recaptcha.net/recaptcha)。

由于 reCaptcha 国内镜像是可以直接连接的，而且还是 `Google` 官方的镜像，所以就能正常加载了。

另外，这个方案还会修改页面的 `Content-Security-Policy` (内容安全政策) 设置，使得有 `Content-Security-Policy` 的页面的 `reCaptcha` 能正常加载。

---

**THE END**感谢您的阅读\~
