---
title: Windows-Linux子系统：快速入门
date: 2023-01-03 12:09:40
tags:
- Backend
- Linux
- 编程
categories:
- [编程,后端,WSL]
---

`Ubuntu`是一个以桌面应用为主的`Linux`操作系统，很久以前我就听说过它的大名。但当我询问如何在`Windows`系统里面安装一个时，我才得知要使用`VM Ware`等虚拟机软件，我也就没有去折腾了。不过买新电脑之后发现`Win10`自带一个`Windows Subsystem for Linux`的虚拟机功能，就来尝试一下。期间我也遇到了占用空间过大，`apt`速度慢等问题，这里也顺带说一下解决方案。

~~但其实到最后我发现装了这个`Ubuntu`，除了对`Shell Script`的原生支持以外，对我也没有多少用处（~~

<!--more-->

## 1. 安装`WSL`与`Ubuntu`

要安装`WSL`，我们首先需要用管理员权限在`powershell`中打开两个功能，分别是`WSL`本身和虚拟化：

```powershell
dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
```

这个时候我们用`wsl`这个命令来检查一下是否可用。如果一切正常，使用`wsl --install`命令就可以安装最新版本的`Ubuntu`。如果你不想安装`Ubuntu`而是别的系统的话，可以使用如下语法：

```powershell
wsl --install -d <Version>
```

等安装完毕，之后的话就是设置用户名和密码，这里就不细说了。

***

## 2. 转移`Ubuntu`文件位置

之后你就可以用`apt`来安装你需要的包了，不过安装几个较大的包比如`nodejs`和`python`之后，你会发现`C`盘突然被`Ubuntu`占用了很多，像我一下子就60%~70%。这个时候我就打算把`Ubuntu`移到`D`盘去，幸运的是，这只需要几个步骤。

首先，`wsl -l`获取自己的`Ubuntu`版本号，像我是`Ubuntu-20.04`。然后我们停止系统的运行，导出整个系统，并反注册。`wsl`会生成一个打包的`tar`文件，我们再导入即可：

```powershell
wsl --export Ubuntu-20.04 d://ProgramFiles//Ubuntu//ubuntu-20.04.tar
wsl --unregister Ubuntu-20.04
wsl --import Ubuntu-20.04 d://wslubuntu//Ubuntu d://ProgramFiles//Ubuntu//ubuntu-20.04.tar
```

然后我们用`wsl`命令来看一下是否注册成功。但这个时候有个问题：你的用户名变成了`root`。这个时候我们在`Ubuntu`里面执行：

```bash
myUsername=<username>
echo -e "[user]\ndefault=$myUsername" >> /etc/wsl.conf
```

就可以把名字改回来。之前生成的系统`tar`文件也就可以删除了。最后我们用管理员权限打开`powershell`重启`Ubuntu`系统，来应用所有更改：

```powershell
net stop LxssManager
net start LxssManager
```

（`wsl`的运行依靠`LxssManager`，具体也不用太管）

***

## 3. 修改`Ubuntu`镜像源

首先进入`apt`的文件夹：

```bash
cd /etc/apt/
```

然后对原先的配置文件做一个镜像，

```bash
sudo cp -a sources.list sources.backup.list
```

到清华镜像官方获取到`ubuntu`的链接，比如`20.04`是这样：

```
# 默认注释了源码镜像以提高 apt update 速度，如有需要可自行取消注释
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-updates main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-updates main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-backports main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-backports main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-security main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-security main restricted universe multiverse

# 预发布软件源，不建议启用
# deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-proposed main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-proposed main restricted universe multiverse
```

然后用`vim`或`nano`编辑`sources.list`，清空后全部粘贴，保存退出。重启`wsl`，并使用

```bash
sudo apt update
```

来确认是否切换到清华的镜像源了。

****

## 4. 安装`xfce4`图形界面

既然有了命令行的`Ubuntu`，我们能不能拥有它的`GUI`呢？~~我们可以借助`xfce4`搭配远程桌面来搭建一个图形界面。~~

**这里不建议使用`xfce4`，容易黑屏、报错，建议直接参考第5步，安装`gnome`桌面。**

### 4.1 安装依赖

安装`xrdp`、`xfce4`和`xfce4-goodies`。中间一路回车即可（会有一个粉色的界面）。

```bash
sudo apt install xrdp xfce4 xfce4-goodies
```

### 4.2 修改`xrdp`配置

先对原配置做一个备份：

```bash
sudo cp /etc/xrdp/xrdp.ini /etc/xrdp/xrdp.ini.bak
```

然后，执行

```bash
sudo sed -i 's/3389/3390/g' /etc/xrdp/xrdp.ini
sudo sed -i 's/max_bpp=32/#max_bbp=32\nmax_bpp=128/g' /etc/xrdp/xrdp.ini
sudo sed -i 's/xservervpp=24/#xservervpp=24\nxserverbpp=128/g' /etc/xrdp/xrdp.ini
```

就会自动修改。然后执行

```bash
echo xfce4-session > ~/.xsession
sudo nano /etc/xrdp/startwm.sh
```

把光标移到文件的最后两行，用`#`号注释掉，然后新增两行，最后效果如下：

```bash
# test -x /etc/X11/Xsession && exec /etc/X11/Xsession
# exec /binsh /etc/X11/Xsession

# xfce
startxfce4
```

保存并退出（<kbd>Ctrl+X</kbd>，按`y`并回车，退出）。

### 4.3 启动远程桌面

首先复制如下代码：

```bash
sudo /etc/init.d/xrdp start
```

然后`vim`或`nano`打开`bash.bashrc`添加一个别名：

```bash
alias remote="sudo /etc/init.d/xrdp start"
```

重启`wsl`。然后输入`remote`，就会启动服务器。用`Win10`自带的远程桌面连接`localhost:3390`，会跳出来一个蓝色框，输入自己`Ubuntu`的用户名和密码，就可以进入`Ubuntu`的远程桌面了。

***

## 5. `gnome`图形界面

这个`gnome`图形界面是要求`WSL2`的，如果你是`Win10`则默认是`WSL1`。先确认一下：

```powershell
wsl -l -v
```

如果是`WSL1`的话则需要安装升级包：[微软官网](https://learn.microsoft.com/zh-cn/windows/wsl/install-manual#step-4---download-the-linux-kernel-update-package)，下载下来安装即可。然后管理员执行：

```powershell
wsl --set-version Ubuntu-20.04 2 
```

它就会自动升级为`WSL2`。然后进入`wsl`，执行

```bash
sudo apt update
sudo apt install git
git clone https://github.com/DamionGans/ubuntu-wsl2-systemd-script.git
cd ubuntu-wsl2-systemd-script/
bash ubuntu-wsl2-systemd-script.sh
```

来安装依赖`systemd`。安装好之后重启：

```powershell
wsl --shutdown
wsl
```

输入

```bash
systemctl
```

如果它不回复你

> System has not been booted with systemd as init system (PID 1). Can't operate.

那就说明你做对了，随后我们来安装`gnome`桌面（确保你已经把`Ubuntu`切换到了`D`盘或其他，因为会占用3个`G`左右）：

```bash
sudo apt update
sudo apt install -y ubuntu-desktop
```

然后安装`xrdp`：

```bash
sudo apt install -y xrdp
sudo adduser xrdp ssl-cert
sudo systemctl restart xrdp
```

配置防火墙：

```bash
sudo ufw allow 3389
```

这个时候远程连接`localhost:3389`即可。会要求你输入账号密码，进入图形界面后还是要你输入密码。如果一切正常的话，你的`gnome`图形界面就安装成功了！

**注：如果你在升级`WSL2`后发现`sudo apt update`卡死了，别怕重装一次`Ubuntu`，重新执行1~3步即可。**

***

至此，你已经拥有了`WSL`中的`Ubuntu`，并且更改了镜像源，成功地开启了远程桌面。听说`Linux`系统中有意思的命令还挺多的，那下一篇文章就来讲讲这个。

***

**致谢**

这里写一下我参考到的文章：

1. [Win10 安装wsl并将文件位置从C盘迁移至D盘_快乐啊啊啊啊啊的博客-CSDN博客_wsl迁移到d盘](https://blog.csdn.net/weixin_50321412/article/details/124592284)

2. [windows下重启wsl_天已青色等烟雨来的博客-CSDN博客_wsl reboot](https://blog.csdn.net/x356982611/article/details/107782513?spm=1001.2101.3001.6661.1&utm_medium=distribute.pc_relevant_t0.none-task-blog-2%7Edefault%7ECTRLIST%7Edefault-1-107782513-blog-108133340.pc_relevant_default&depth_1-utm_source=distribute.pc_relevant_t0.none-task-blog-2%7Edefault%7ECTRLIST%7Edefault-1-107782513-blog-108133340.pc_relevant_default&utm_relevant_index=1)

3. [更改手动导入的wsl的默认登录用户_skyandcloud-pal的博客-CSDN博客_wsl修改默认用户](https://blog.csdn.net/qq_41667316/article/details/120931194)

4. [WSL GUI图形界面(xfce4)的安装 - 简书](https://www.jianshu.com/p/af94731626e3)

5. [wsl安装ubuntu并设置gnome图形界面详细步骤（win11+ubuntu18）_heusjh的博客-CSDN博客_wsl安装gnome桌面](https://blog.csdn.net/m0_51194302/article/details/127891929)

**THE END**感谢您的阅读\~
