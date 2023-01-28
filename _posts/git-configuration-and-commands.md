---
title: 【转】关于Git你需要知道的一切
date: 2022-09-25 13:45:35
tags:
- GitHub
- Git
categories:
- [GitHub, 命令行]
nocopyright: true
---

暂且记录一下，作为一个备忘录，方便之后查阅。也可作为初学者上手用。主要还是之前创作过程中提到了需要使用`Git`哦。

> 原文链接：
> 
> [git配置及常见命令_星辰浩宇的博客-CSDN博客_git配置命令](https://blog.csdn.net/amf12345/article/details/121048818)
> 
> [Git常用配置命令_油泼刀削面的博客-CSDN博客_git 配置命令](https://blog.csdn.net/Bwen_F/article/details/125007378)

<!--more-->

## 1. 安装后的配置

安装`Git`后，我们需要本地`Git`与远程`GitHub`连接的建立，只有将`Git`本地与远程的`GitHub`建立了连接以后我们本地的项目才能上传至远程服务器。

注：下面的命令请使用自己的用户名密码替换

### 1.1 在`Git`中配置全局的`GitHub`账号信息

```powershell
git config --global user.name "username"
git config --global user.email "email"
```

### 1.2 生成`RSA`公、私钥文件

```powershell
ssh-keygen -t rsa -C "email"
```

### 1.3 配对公、私钥

命令执行成功后，在本地电脑的名为`.ssh`的目录下（例如`C:\Users\gulei\.ssh\`）找到名为`id_rsa.pub`的文件，打开这个文件后将里面的内容先复制下来。

![](https://s1.ax1x.com/2022/09/25/xEoIk6.png)

然后我们找到`GitHub Settings`<https://github.com/settings/keys>：

![](https://s1.ax1x.com/2022/09/25/xEootK.png)

在左边的栏目中选择`SSH and GPG Keys`：然后在出来的右边的框框中选择 `New SSH`：其中`Title`可以随意写个名字，`Key`里面的内容需要把刚刚复制的id_rsa.pub文件中的内容拷贝进去，最后点击`Add SSH key`即可。 

![](https://s1.ax1x.com/2022/09/25/xEoTfO.png)

我们如何检测是否已经连接上了呢？使用以下命令：

```powershell
ssh -T git@github.com
```

![](https://s1.ax1x.com/2022/09/25/xE7qeA.png)

---

## 2. 命令列表

![](https://s1.ax1x.com/2022/09/25/xE7HLd.png)

说明：

`workspace`：工作区

`staging area`：暂存区/缓存区

`local repository`：版本库或本地仓库

`remote repository`：远程仓库

1、查看用户名和邮箱地址：

```powershell
git config user.name
git config user.email
```

2、修改用户名和邮箱地址

```powershell
git config --global user.name  "xxxx" 
git config --global user.email  "xxxx"  
```

3、如果我们是直接拉下代码库

```powershell
git clone url
```

那么我们这个文件夹本身已经就是一个`git`仓库了

4、如果我们是本地已有的文件去与远程代码库相关联的话，需要执行以下步骤：

```powershell
cd 文件/   #即需要进入这个文件
git init   #将文件初始化为git文件
#与远程代码库添加链接
git remote add origin 代码库链接
#后续提交过程都一样
```

5、查看本地分支

```powershell
git branch
```

注:名称前面加* 号的是当前的分支

6、在本地创建新的分支并切换到该分支上

```powershell
git checkout -b private
```

等价于

```powershell
git branch private       #在本地新创建private分支
git checkout private     #切换到新分支上
```

7、查看远程分支

```powershell
git branch -r
```

8、查看所有的分支（包括本地分支以及远程分支）

```powershell
git branch -a
```

加上`-a`参数可以查看远程分支，远程分支会用红色表示出来（如果你开了颜色支持的话）

9、查看本地分支与远程分支的映射关系

```powershell
git branch -vv
```

10、重命名本地分支

```powershell
git branch -m  
```

11、删除本地分支

```powershell
git branch -d name
```

12、删除远程分支

```powershell
git branch -r -d origin/name
git push origin:name  #删除后还需要推送到远程
```

13、查看当前远程仓库信息

```powershell
git remote -vv
```

14、远程新建分支后，本地查看不到，使用以下命令同步

远程新建分支，本地在未创建此新分支前便已经`clone`下来，现在本地查看分支时没有发现远程新建的 分支，使用如下命令更新，即可查看远程新建的分支

```powershell
git remote #列出远程主机
git remote update origin --prune  #更新远程主机origin整理分支
```

15、当我们手动在远程分支上建立了一个新的分支，本地也有一个新的分支时，想要本地的新分支提交到这个远程的新分支上时，我们需要新建本地分支与远程分支的关联

```powershell
git branch --set-upstream-to=origin/name name
```

eg：我的本地新建了一个分支`private`远程新建了一个分支`dev`把二者进行关联起来

```powershell
git branch --set-upstream-to=origin/dev private
或者
git branch -u orgin/dev private
```

如果此时已经在本地private分支上，可以直接

```powershell
git branch -u origin/dev
```

输出：Branch `private` set up to track remote branch `dev` from `origin`.

16、如果本地有分支，但是远程没有分支对应，如何把本地的分支提交到远程

假设有本地分支`dev`，远端没有该分支。此时`push`或者`pull`时，就不知道跟踪的是哪个分支。使用以下指令：

```powershell
git push --set-upstream origin dev
```

推送后远程也会出现`dev`分支,二者建立连接，注意此时的`dev`并不是你给远程分支起的名字，而是根据本地的分支推送上去的远程分支。后续`push`和`pull`时，就不用指定分支。

17、本地没有某个分支，远程仓库有此分支，怎样拉取远端分支代码到本地分支？

```powershell
git checkout --track origin/name
```

此时，本地会自动创建分支`name`与远端分支同名，并与远端分支`name`关联。

建议在弄分支的时候最好本地与远程的名字相同便于区别

18、如果我们的本地文件已经关联了远程代码仓库，现在想关联新的代码仓库

一种方法是将原来的远程仓库重新命名，另一种是删除原来的远程仓库；二者选其一，然后再新关联现在的远程仓库即可

```powershell
#方法一：重命名原来的远程仓库
git remote rename origin old-origin

#方法二：删除原来的远程仓库
git remote rm origin

#上面的二选一，然后重新指定新的源
git remote add origin [url]
```

19、撤销本地分支与远程分支的映射关系

```powershell
git branch --unset-upstream
```

此时，当前的本地分支与远程分支解除关系

20、`Git`在本地新建分支后，可做远程分支关联。关联目的是，如果在本地分支下进行`pull`和`push`操作时 ，便不需要指定远程的分支。

21、新建本地分支与远程分支相关联

```powershell
git checkout -b dev origin/dev   # 新建本地分支dev与远程dev分支相关联
```

22、执行`push`推送代码

```powershell
git push
```

23、本地分支`push`到远程分支

本地分支 `v2` 远程分支`dev`

如果没有建立关系时

```powershell
git push origin v2:dev
或者
git push origin dev #本地已经在v2分支上
```

如果已经建立关联 且目前的本地分支就在`v2`上，我们可以直接使用

```powershell
git push
```

24、多人合作提交代码

在我们自己提交之前如果有别人提交了代码，我们需要先进行合并代码，再进行`push`

```powershell
方案一：合并远程分支代码
git fetch origin 
(git remote update有的时候可能需要同步一下远程和本地）
git merge origin/远程分支名　　
方案二：合并远程分支代码
git pull origin 远程分支名
（PS：方案一和方案二选择一个即可）
执行push推送代码
git push origin 本地分支名:远程分支名
```

25、`git fetch`与 `git pull`的区别

`git fetch`是将远程主机的最新内容拉到本地，用户在检查了以后决定是否合并到工作本机分支中。

而`git pull`则是将远程主机的最新内容拉下来后直接合并，即：`git pull = git fetch + git merge`，这样可能会产生冲突。

26、`git fetch`的常见命令如下：

```powershell
git fetch <远程主机名> //这个命令将某个远程主机的更新全部取回本地，一般远程主机名为origin
git fetch <远程主机名> <分支名> //注意之间有空格,返回的是特定分支的更新
```

例如：返回`origin`主机的`maste`分支的更新 `git fetch origin master` 
取回更新后，会返回一个`FETCH_HEAD`，指的是某个`branch`在服务器上的最新状态，我们可以在本地通过它查看刚取回的更新信息：

```powershell
git log -p FETCH_HEAD
```

可以看到返回的信息包括更新的文件名，更新的作者和时间，以及更新的代码（红色删除和绿色新增）。

我们可以通过这些信息来判断是否产生冲突，以确定是否将更新`merge`到当前分支。

如果我们需要合并的话执行以下代码

```powershell
git merge FETCH_HEAD
```

总结：`fetch`合并到分支需要两步

```powershell
git fetch origin master //从远程主机的master分支拉取最新内容  
git merge FETCH_HEAD    //将拉取下来的最新内容合并到当前所在的分支中
```

27、`git pull`的常见用法

将远程主机的某个分支的更新取回，并与本地指定的分支合并

```powershell
git pull <远程主机名> <远程分支名>:<本地分支名>
```

如果需要合并的本地分支就是目前的分支，则后面的本地分支名可以省略

28、还原代码至某个版本

```powershell
git reset --hard 版本号
```

如果不加版本号，默认恢复上一个版本

29、合并分支到`master`上

首先切换到`master`分支上

```powershell
git checkout master
```

如果是多人开发的话 需要把远程`master`上的代码`pull`下来

```powershell
git pull origin master
```

然后我们把`dev`分支的代码合并到`master`上

```powershell
git merge dev
```

30、查看状态

```powershell
git status
```

31、git配置的一些其他的命令

```powershell
git log                                         # 查看提交历史 
git config core.ignorecase false                # 设置大小写敏感
```

32、git的提交

```powershell
git diff                        # 查看变更内容 
git add .                       # 跟踪所有改动过的文件 
git add                         # 跟踪指定的文件 
git mv                          # 文件改名 
git rm                          # 删除文件 
git rm --cached                 # 停止跟踪文件但不删除 
git commit -m "commit message"  # 提交所有更新过的文件 
git commit --amend              # 修改最后一次提交
```

33.查看历史

```powershell
git log                         # 查看提交历史 
git log -p                      # 查看指定文件的提交历史 
git blame                       # 以列表方式查看指定文件的提交历史
```

34.撤销

```powershell
git reset --hard HEAD           # 撤消工作目录中所有未提交文件的修改内容
git reset --hard                # 撤销到某个特定版本 
git checkout HEAD               # 撤消指定的未提交文件的修改内容 
git checkout --                 # 同上一个命令 
git revert                      # 撤消指定的提交分支与标签
```

35.分支与标签

```powershell
git branch                      # 显示所有本地分支 
git checkout                    # 切换到指定分支或标签 
git branch                      # 创建新分支 
git branch -d                   # 删除本地分支 
git tag                         # 列出所有本地标签 
git tag                         # 基于最新提交创建标签 
git tag -a "v1.0" -m "一些说明"  # -a指定标签名称，-m指定标签说明 
git tag -d                      # 删除标签  
git checkout dev                # 合并特定的commit到dev分支上 
git cherry-pick 62ecb3
```

36.合并与衍合

```powershell
git merge                       # 合并指定分支到当前分支 
git merge --abort               # 取消当前合并，重建合并前状态 
git merge dev -Xtheirs          # 以合并dev分支到当前分支，有冲突则以dev分支为准
git rebase                      # 衍合指定分支到当前分支
```

37.远程操作

```powershell
git remote -v                   # 查看远程版本库信息 
git remote show                 # 查看指定远程版本库信息 
git remote add                  # 添加远程版本库 
git remote remove               # 删除指定的远程版本库 
git fetch                       # 从远程库获取代码 
git pull                        # 下载代码及快速合并 
git push                        # 上传代码及快速合并
```

38.打包

```powershell
git archive --format=zip --output ../file.zip master    # 将master分支打包成file.zip文件，保存在上一级目录 
git archive --format=zip --output ../v1.2.zip v1.2      # 打包v1.2标签的文件，保存在上一级目录v1.2.zip文件中 
git archive --format=zip v1.2 > ../v1.2.zip             # 作用同上一条命令
```

39.远程与本地合并

```powershell
git init                              # 初始化本地代码仓 
git add .                             # 添加本地代码 
git commit -m "add local source"      # 提交本地代码 
git pull origin master                # 下载远程代码 
git merge master                      # 合并master分支
git push -u origin master             # 上传代码
```

---

## 3. `.gitignore`文件

在主目录下创建 .gitignore 文件

1. 忽略文件中的空行或以井号（`#`）开始的行将会被忽略。

2. 可以使用Linux通配符。例如：星号（`*`）代表任意多个字符，问号（`?`）代表一个字符，方括号（`[abc]`）代表可选字符范围，大括号（`{string1,string2,…}`）代表可选的字符串等。

3. 如果名称的最前面有一个感叹号（`!`），表示例外规则，将不被忽略。

4. 如果名称的最前面是一个路径分隔符（`/`），表示要忽略的文件在此目录下，而子目录中的文件不忽略。

5. 如果名称的最后面是一个路径分隔符（`/`），表示要忽略的是此目录下该名称的子目录，而非文件（默认文件或目录都忽略）。
   
   ```gitignore
   #为注释 
   *.txt #忽略所有 .txt结尾的文件,这样的话上传就不会被选中！
   !lib.txt #但lib.txt除外
   /temp #仅忽略项目根目录下的TODO文件,不包括其它目录temp
   build/ #忽略build/目录下的所有文件
   doc/*.txt #会忽略 doc/notes.txt 但不包括 doc/server/arch.txt
   ```

---

**THE END**感谢您的阅读\~
