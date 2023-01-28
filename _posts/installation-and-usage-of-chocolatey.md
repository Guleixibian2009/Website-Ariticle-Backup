---
title: Chocolatey——Windows上的“APT” 
date: 2023-01-12 08:36:07
tags:
- 软件
- 命令行
categories:
- [编程,命令行]
---

在`Ubuntu`平台上，安装软件有一种极其方便的思路——`APT`。用命令行管理电脑上安装的软件，既方便，又显得很酷。我就寻思了——`Windows`平台上有没有类似的替代软件呢？

肯定是有的。这个软件，叫做“巧克力”`Chocolatey`。最酷的一点是，它连安装都是一个命令即可。

<!--more-->

## 1. 安装`Chocolatey`

```powershell
Set-ExecutionPolicy Bypass -Scope Process -Force; iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))
```

这个命令来自官网。只需要管理员权限打开`Powershell`并复制粘贴执行即可。安装完场之后，可以使用

```powershell
choco -v
```

检查安装情况。

****

## 2. 用`Choco`安装软件

用`Choco`安装软件只需要两步。首先我们管理员权限打开`Powershell`，使用

```powershell
choco find/list/search <package>
```

来寻找你需要的包。然后一般大众的编程类的软件都可以这么安装，一些功能类的软件也可以。当然这里要提醒一点，不要用`Choco`安装`vscode`，会极其的慢，建议按照[我之前的文章](https://guleixibian2009.github.io/2022/09/26/more-ways-to-speed-up/#3-VS-Code%E4%B8%8B%E8%BD%BDCDN%E9%93%BE%E6%8E%A5)快速安装`vscode`。

然后使用简写安装软件：

```powershell
cinst -y <package>
```

如果是卸载的话，直接

```powershell
choco uninstall <package>
```

就可以卸载。

****

## 3. 用`Choco`更新软件

```powershell
choco upgrade <package>
```

就可以更新某个软件。如果想要一件全部更新，可以使用：

```powershell
choco upgrade all
```

****

## 4. 我的软件安装在哪里？

默认情况下，安装的软件会在

```
C:\ProgramData\chocolatey
```

这个目录下。有一些软件会被自动移到`Program Files`文件夹里。

****

从此以后，再也不用费尽心思找软件、找更新力！（

**THE END**感谢您的阅读\~
