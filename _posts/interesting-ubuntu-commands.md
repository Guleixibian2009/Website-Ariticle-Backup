---
title: 那些有趣的Linux命令，你都试过几个？
date: 2023-01-04 12:22:53
tags:
- 编程
- Backend
- Linux
categories:
- [编程,后端,WSL]
---

OK那么既然我们安装好了`WSL`和`Ubuntu`，也成功地打开了它的`Gnome`图形界面，肯定要来体验一下，这一篇文章也是在`WSL`里面写的。不过在干活之前我也是找了一些有意思的命令，来熟悉一下`Ubuntu`的环境，比如：

![](https://s1.ax1x.com/2023/01/04/pSFYEjA.png)

**注：除非特殊提醒，文中提到的包都可以使用`apt`安装。**

<!--more-->

## 1. 字符(画)相关

### 1.1 `cmatrix`与黑客帝国

我想，各位如果喜欢科幻的话，一定对《黑客帝国》里的字符雨并不陌生。但其实，只需要一个指令，就可以让你的`terminal`里下起字符雨。

```bash
sudo apt install cmatrix
cmatrix
```

### 1.2 火！火！火！

让自己的终端燃起来……

```bash
sudo apt install libaa-bin
aafire
```

这个指令会新建一个窗口，它就会以字符画的方式“燃”起来。

![](https://s1.ax1x.com/2023/01/04/pSFYk1H.png)

### 1.3 当你把`ls`打反

手速过快是一件很痛苦的事情，尤其当你把`ls`打成了~~死了~~`sl`。`Stream Locomotive`这个命令会在你的屏幕上画一列火车（且不能用<kbd>Ctrl+C</kbd>强制停止）

![](https://s1.ax1x.com/2023/01/04/pSFYtH0.png)

先用`apt`安装，然后会有额外的一步，把`/usr/games`这个路径加到`$PATH`里面去，先复制这段代码:

```bash
export PATH="$PATH:/usr/games"
```

然后

```bash
gedit ~/.bashrc
```

把刚才那行粘贴到文件末尾，然后

```bash
source ~/.bashrc
```

刷新一下，就可以使用`sl`了。

*不过，如果你经常打错的话，建议还是不要安装，否则……*

### 1.4 彩色字生成器`toilet`

需要显示一个大标题吗？`toilet`可以满足你的需求：

![](https://s1.ax1x.com/2023/01/04/pSFYeBt.png)

### 1.5 牛牛也会说话

![](https://s1.ax1x.com/2023/01/04/pSFYCtO.png)

嗯……这头牛是怎么学会说话的？`cowsay`这个指令教了很多动物说话，比如：

![](https://s1.ax1x.com/2023/01/04/pSFYPhD.png)

这个还有高级版本`xcowsay`：

![](https://s1.ax1x.com/2023/01/04/pSFYmHP.png)

### 1.6 每日一句`fortune`

这个有点像日签，每次执行`fortune`都会跳出来一句名言或鸡汤：

![](https://s1.ax1x.com/2023/01/04/pSFY9AK.png)

你也可以把它和`cowsay`一起用，就会变成牛牛日签~

```bash
fortune | cowsay
```

### 1.7 彩色的牛牛？！

在`Ubuntu`里面有个命令叫`lolcat`，可以把任何输出变成彩虹色的：

![](https://s1.ax1x.com/2023/01/04/pSFYZnI.png)

然后搭配之前几个命令，你就可以拥有……彩虹色的牛牛日签

### 1.8 循·环·输·出

这是一个自带的系统命令：

```bash
yes Hello, world!
```

就会不停的打印`Hello, world!`。如果搭配`lolcat`使用……

![](https://s1.ax1x.com/2023/01/04/pSFYuAf.png)

### 1.9 超级牛力

这个是`apt`的老梗了。`apt moo`这个彩蛋，自己去揭晓~

***

## 2. 功能性指令

说了这么多看似没用的命令，也顺带说一些有用的指令，让你平时也能用上它们：

### 2.1 日历

`Ubuntu`是有日历的，但是如果你想看很久之前或很久之后的，需要点很多次。这个时候自带的`cal`命令就能派上用场，比如：

![](https://s1.ax1x.com/2023/01/04/pSFBs7d.png)

### 2.2 质因数分解

这个的话对我这种学生党还是有那么一点用的，比如像非常大的数，很快就能分解开：

![](https://s1.ax1x.com/2023/01/04/pSFB6AA.png)

### 2.3 系统信息

安装了`screenfetch`后，就可以很方便的展示自己的系统信息了，方便技术人员进行一些工作：

![](https://s1.ax1x.com/2023/01/04/pSFBght.png)

### 2.4 从删库到跑路

```bash
sudo rm -rf /*
```

千万不要轻易尝试……不用我多说

***

## 3. 和鼠标有关的有趣指令

### 3.1 追随鼠标的小猫`oneko`

无聊的时候，就让小猫陪你玩一会儿：

![](https://s1.ax1x.com/2023/01/04/pSFBctI.png)

小猫会一张尝试跑到你的鼠标边，然后坐下来。你再动，它又会跑起来，乐此不疲。

### 3.2 盯着鼠标看的眼睛

![](https://s1.ax1x.com/2023/01/04/pSFBR9P.png)

```bash
sudo apt install x11-apps
```

安装之后就可以用`xeyes`来唤起一双盯着鼠标看的大眼睛了。

***

这么一盘点，发现`Ubuntu`的有趣命令比`Windows`多多了。此外在写作过程中我也学会了用`gnome-screenshot -i`来截图，可谓是一举多得。

**参考资料：**

[28条超有趣的Linux命令 | 程序师 - 程序员、编程语言、软件开发、编程技术](https://www.techug.com/post/29-funny-linux-tips/)

**THE END**感谢您的阅读~
