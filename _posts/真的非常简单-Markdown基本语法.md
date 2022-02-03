---
title: 真的非常简单-Markdown基本语法
date: 2021-08-25 14:46:50
tags:
- Markdown
- 编程
- 语法
categories:
- [ 编程,Markdown,Markdown语法 ]
---

在很多博客、论坛，包括`Github Pages`(参见[这篇文章](https://guleixibian2009.github.io/2021/08/15/GithubPages-简单易上手的网站制作-Jekyll版/)) 里都有大量运用到一种叫做`Markdown`的文本语言。不管你是在创建自己的网站、写文章，一般平台都需要写`Markdown`。如果你想学习`Markdown`，你算是来对地方了！

<!-- more -->

## 0. `Markdown` 是什么？

>`Markdown`是一种轻量级标记语言，创始人为约翰·格鲁伯(英语:John Gruber)。  
>它允许人们使用易读易写的纯文本格式编写文档，然后转换成有效的`XHTML`(或者`HTML`)文档。这种语言吸收了很多在电子邮件中已有的纯文本标记的特性。  
>由于`Markdown`的轻量化、易读易写特性，并且对于图片，图表、数学式都有支持，目前许多网站都广泛使用`Markdown`来撰写帮助文档或是用于论坛上发表消息。如`GitHub`、`OpenStreetMap` 、`SourceForge`、简书等，甚至还能被使用来撰写电子书。    
>（摘自百度百科）  

___

## 1. 文章标题&小标题
### 1.1 像`HTML`一样写标题
在`HTML`里，标题分六级：

```HTML
<h1>This is an H1</h1>
<h2>This is an H2</h2>
<h3>This is an H3</h3>
...
```

相对应的，`Markdown`标题也分六级。

```markdown
# This is an H1  
## This is an H2  
...  
###### This is an H6  
```

就像你看到的那样，每层标题就是几个**`#`**。

### 1.2 `Markdown`专属标题
不过，在`Markdown`中表示标题也可以用一种特殊的方式。

```Markdown

This is an H1
=============

This is an H2
-------------

```
不过它本身只支持2种标题，即大、小标题。

___
## 2. 文字样式语法
在`Markdown`中，文字可以是*斜体*、**粗体**、***粗斜体***,~~删除线~~，<u>下划线</u>。

### 2.1 基本样式
- 斜体用一个`*`包围，就像` *这是斜体* `，显示出来就是 *这是斜体* 

- 粗体用两个`*`包围，就像` **这是粗体** `，显示出来就是 **这是粗体**

- 粗斜体用三个`*`包围，就像` ***这是粗斜体*** `，显示出来就是 ***这是粗斜体***

  （本质上它其实就是**粗体**包住了*斜体*，所以***你交学费***了吗）

- 删除线用两个`~`包围，就像` ~~这是删除线~~ `，显示出来就是 ~~这是删除线~~

### 2.2 某些来自`HTML`的样式

> 由于`Markdown`可以直接转换成`HTML`（在百科里说过了），所以有很多`HTML`标签都可以在`Markdown`中使用。比如说，`<u>` `<kbd>` `<script>` 。**他们会直接被插入生成的`HTML`文件中**。

#### 2.2.1 瞎划线（下划线）
下划线是用`HTML`实现的，在`HTML`里下划线是` <u> `,所以语法就是` <u>这是下划线</u> `,显示出来就是<u>这是下划线</u>  

#### 2.2.2 颜色
如果<font color=green> 你 </font>需要给文字调 <font color=red> 颜色 </font> ，可以用 ` <font> ` 标签，语法为
```HTML
<font color=red> Some text </font>
```

这个`<font>`标签接收一个参数`color`。你可以把它设为一些常见的颜色，比如

|            颜色            |                    效果                    |
| :------------------------: | :----------------------------------------: |
|     `<font color=Red>`     |         <font color=Red>Red</font>         |
|   `<font color=Yellow>`    |      <font color=Yellow>Yellow</font>      |
|    `<font color=Blue>`     |        <font color=Blue>Blue</font>        |
|    `<font color=Green>`    |       <font color=Green>Green</font>       |
|    `<font color=Gold>`     |        <font color=Gold>Gold</font>        |
|    `<font color=Grey>`     |        <font color=Grey>Grey</font>        |
|   `<font color=Purple>`    |      <font color=Purple>Purple</font>      |
|    `<font color=Azure>`    |       <font color=Azure>Azure</font>       |
| `<font color=GreenYellow>` | <font color=GreenYellow>GreenYellow</font> |

如果你还想要其他的颜色，你可以访问 <https://www.w3school.com.cn/tags/html_ref_colornames.asp> 来研究更多颜色~

### 2.3 脚注

这是一个脚注 [^1] 。脚注的语法是：
```Markdown
TextTextText [^name] TextTextText
```

___
## 3. 链接与图片

### 3.1 链接
文章中的“链接”指“超链接”。 [这是一个超链接实例](https://guleixibian2009.github.io/) ，它指向我的主页。  
链接的语法为 

```Markdown
[Name](Place) 
```

### 3.2 图片
图片的语法和链接很相似，只是在` [Name](Place)` 之前加上一个 \! (记住都是英文标点！！！),如

```Markdown
![Name](Place "替代名")
```

___
## 4. 列表
在`Markdown`中，列表分两种：有序的，和无序的（还有 “待办事项” ！他属于无序列表）。

### 4.1 有序列表
有序列表，就像  
```Markdown
1. 第一个元素  
2. 第二个元素  
3. 第三个元素
```
在`Markdown`中，直接打 `1.` 就会出现一个有序列表。当然， `i.` `a.` 甚至不从头开始也可以：



### 4.2 无序列表
无序列表的原理和有序列表一样，不过不以 `1.` 打头，而是：

```Markdown
- 第一种方式
- 第一种方式
```

```Markdown
+ 第二种方式
+ 第二种方式
```

```Markdown
* 第三种方式
* 第三种方式
```
显示出来都是
- 无序列表
- 无序列表

### 4.3 `To do list`
通过无序列表我们还可以创建一个任务表（`To do list`），如下：

- [x]  No.1
- [ ]  No.2
- [x]  No.3

语法如下：
```Markdown
[x] No.1
[ ] No.2
[x] No.3
```
其中 [x] 表示“已完成”，[] 表示“未完成”。

### 4.4 合并列表


---
## 注释
以下是注释内容：  

[^1]: 你学废了吗？


___
