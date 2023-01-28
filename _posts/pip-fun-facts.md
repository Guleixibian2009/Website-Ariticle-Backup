---
title: Python Pip常见问题与Package推荐
date: 2023-01-09 10:37:26
tags:
- Python
categories:
- [编程,Python]
---

从开始自学编程到现在，我接触最多的还是`Python`。用`Python`就免不了要用到`Pip`，在这个过程中我算是踩了三个大坑；与此同时我也找到了几个极其有用的`Package`，也跟大家分享一下。

省流：`Pip`换源、非管理员升级`Pip`失败问题、`requirements.txt`的生成、`PyInstaller`打包可执行文件；附赠`bilili`B站爬虫！

**注：爬虫下载到的视频仅供学习用，千万不可作商用用途，使用过程中如有问题、造成损失，本人概不负责。**

<!--more-->

## 1. `Pip`换源

这个我之前应该讲过，这里还是再放一下：

`Pypi`官方的源在国内是很慢的，速度大概在`KB`级。我们需要调整它的镜像源，比如国内的阿里云。

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

****

## 2. 非管理员更新`Pip`问题解决

`Pip`提示有新版本之后别急着更新，一定要先用管理员权限打开命令行。否则会安装失败，这个时候如果你去用`pip`的话会提示：

```
ModuleNotFoundError: No module named 'pip'
```

这时我们运行：

```powershell
#卸载旧版本的pip，引用python的ensurepip库来安装pip标准库
python -m ensurepip
#更新pip版本
python -m pip install --upgrade pip
```

就可以重新安装`pip`了。这个方法很保险，不会删除已经安装的`package`。

***

## 3. `requirements.txt`的生成

默认情况下，使用

```powershell
pip freeze > requirements.txt
```

是可以导出一个`requirements.txt`的，但是这样会把你安装的所有`Package`都导出，所以不是特别方便。这里还有一种解决方案：`pipreqs`。

```powershell
pipreqs ./ requirements.txt --encoding=utf-8
```

先用`pip`安装`pipreqs`，然后在项目的根目录下执行这个命令就可以自动扫描项目的依赖了。

安装依赖的时候，执行：

```powershell
pip install -r requirements.txt
```

就可以了。

***

## 4. 打包可执行文件

这个需要依赖`pyInstaller`。用`pip`安装之后，找到你想要的文件，然后执行：

```powershell
pyinstaller -F demo.py
```

就可以全自动打包。打包之后在`dist`文件夹里就可以找到打包的文件。

****

## 5. B站爬虫`bilili`

最后推一个发现的`Package`：`bilili`。这是一个B站的爬虫。用法：

```powershell
bilili <url>
```

然后按指引操作就可以免登陆下载到免费视频了。例如：

```powershell
bilili https://www.bilibili.com/video/BV1GJ411x7h7/
```

就可以了。

****

**THE END**感谢您的阅读\~
