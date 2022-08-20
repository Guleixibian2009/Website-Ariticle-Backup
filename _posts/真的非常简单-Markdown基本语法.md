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

> `Markdown`是一种轻量级标记语言，创始人为约翰·格鲁伯(英语:John Gruber)。  
> 它允许人们使用易读易写的纯文本格式编写文档，然后转换成有效的`XHTML`(或者`HTML`)文档。这种语言吸收了很多在电子邮件中已有的纯文本标记的特性。  
> 由于`Markdown`的轻量化、易读易写特性，并且对于图片，图表、数学式都有支持，目前许多网站都广泛使用`Markdown`来撰写帮助文档或是用于论坛上发表消息。如`GitHub`、`OpenStreetMap` 、`SourceForge`、简书等，甚至还能被使用来撰写电子书。    
> （摘自百度百科）  

注：一个好的编辑器是学习的基础。如果你坚持`WYSIWYG`（所见即所得），这里推荐开源项目`MarkText`。官网：<https://github.com/marktext/marktext/>。当然你也可以用`VSCode`或者（付费，虽然超好）`Typora`。

___

## 1. 文章标题&小标题

### 1.1 像`HTML`一样写标题

在`HTML`里，标题分六级：

```html
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

就像你看到的那样，每层标题就是几个 **`#`**。

### 1.2 `Markdown`专属标题

不过，在`Markdown`中表示标题也可以用一种特殊的方式。

```markdown
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
  
  （本质上它其实就是**粗体**包住了*斜体*，所以 ***你交学费*** 了吗）

- 删除线用两个`~`包围，就像` ~~这是删除线~~ `，显示出来就是 ~~这是删除线~~  

- `@mention`：`GFM`中的一种“点名”的方式，其他时候基本没用。

#### 2.1.1 引用块

想要突出显示你引用了某段话？可以使用引用段落！

> 这就是一个简单的引用了！你可以在这里面*使用* **其他**`的语法`。它的语法是：
> 
> ```md
> > 引用引用引用引用引用引用引用引用！
> ```

引用以一个右尖括号开始。一般情况下，我们在多行引用时，会在每一行的开头加一个符号，但如果你懒……

```md
> Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod
> tempor incididunt ut labore et dolore magna aliqua.
```

可以变为：

```md
> Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod  
tempor incididunt ut labore et dolore magna aliqua.
```

> 想要嵌套引用，直接多加一个符号！
> 
> > 嵌套引用中！

```md
> Lorem ipsum...
> > Lorem ipsum...
```

### 2.2 某些来自`HTML`的样式

> 由于`Markdown`可以直接转换成`HTML`（在百科里说过了），所以有很多`HTML`标签都可以在`Markdown`中使用。比如说，`<u>` `<kbd>` `<script>`（当然也不是所有标签都受支持，得看编译器） 。**如果可能，他们会直接被插入生成的`HTML`文件中**。

#### 2.2.1 瞎划线（下划线）

下划线是用`HTML`实现的，在`HTML`里下划线是`<u>`,所以语法就是`<u>这是下划线</u>`,显示出来就是<u>这是下划线</u>。  

#### 2.2.2 颜色

如果<font color=green> 你 </font>需要给文字调 <font color=red> 颜色 </font> ，可以用 `<font>` 标签，语法为

```html
<font color=red> Some text </font>
```

这个`<font>`标签接收一个参数`color`。你可以把它设为一些常见的颜色，比如

| 颜色                         | 效果                                         |
|:--------------------------:|:------------------------------------------:|
| `<font color=Red>`         | <font color=Red>Red</font>                 |
| `<font color=Yellow>`      | <font color=Yellow>Yellow</font>           |
| `<font color=Blue>`        | <font color=Blue>Blue</font>               |
| `<font color=Green>`       | <font color=Green>Green</font>             |
| `<font color=Gold>`        | <font color=Gold>Gold</font>               |
| `<font color=Grey>`        | <font color=Grey>Grey</font>               |
| `<font color=Purple>`      | <font color=Purple>Purple</font>           |
| `<font color=Azure>`       | <font color=Azure>Azure</font>             |
| `<font color=GreenYellow>` | <font color=GreenYellow>GreenYellow</font> |

如果你还想要其他的颜色，你可以访问 <https://www.w3school.com.cn/tags/html_ref_colornames.asp> 来研究更多颜色~  

另外，这其实是一个过时了的`HTML` 标签。所以，我想，还是要避免使用吧。如果可行，可以试试行内`CSS`，即：

```html
<p style="color: red;">Hello World</p>
```

#### 2.2.3 按键？？

听说过`<kbd>`吗？~~（好奇）~~我猜你肯定知道！啊啊，不知道？？？我教你！选中那个`<kbd>`，然后按住<kbd>Ctrl+C</kbd>，选中别处，<kbd>Ctrl+V</kbd>！这就是`<kbd>`了，它表示一种快捷键方式。语法就是：

```html
<kbd>Ctrl+Shift+L</kbd>
```

### 2.3 脚注

这是一个脚注 [^1] 。脚注的语法是：

```Markdown
TextTextText [^name] TextTextText
```

这个脚注一般用数字表示。当然它还有更高级的功能，见下：

___

## 3. 链接与图片

### 3.1 链接

文章中的“链接”指“超链接”。 [这是一个超链接实例](https://guleixibian2009.github.io/) ，它指向我的主页。  
链接的语法为 

```md
[Name](Link) 
<!--示例-->
[主页](https://www.example.com/)
```

想要直接显示这个链接而不显示代替名？可以这样做：

```md
<https://example.com>
```

显示出来就是：<https://example.com>  

想要在一处集中显示所有链接？可以这样使用脚注来替代！

```md
[Example](example)
[example] : https://www.example.com/
```

当然我不太习惯用这个。

### 3.2 图片

图片的语法和链接很相似，只是在` [Name](Place)` 之前加上一个 `!` (都是英文标点),如

```md
![Name](Link "替代名")
<!--示例-->
![Pull Shark](https://github.githubassets.com/images/modules/profile/achievements/pull-shark-default.png "Pull Shark")
```

“替代名”不是必要的，它会被解析为`img`标签的`alt`属性。在方括号`[Pull Shark]`中的内容在有些编译器下会作为一种标题被显示在渲染的图片下面。e.g.

![Pull Shark](https://github.githubassets.com/images/modules/profile/achievements/pull-shark-default.png "Pull Shark")

当然一些高级一些的属性（如居中）还是用`HTML`做出来的！（不知道为什么`Hexo`会自动居中）

___

## 4. 列表

在`Markdown`中，列表分两种：有序的，和无序的。

### 4.1 有序列表

有序列表，就像  

```md
1. 第一个元素  
2. 第二个元素  
3. 第三个元素
```

在`Markdown`中，直接打 `1.` 就会出现一个有序列表。当然， `i.` `a.` 甚至不从头开始也可以：

```md
a. #1
b. #2
c. #3
```

当然这还是取决于你用的编译器啦！

### 4.2 无序列表

无序列表的原理和有序列表一样，不过不以 `1.` 打头，而是：

```md
- 第一种方式
- 第一种方式
```

```md
+ 第二种方式
+ 第二种方式
```

```md
* 第三种方式
* 第三种方式
```

显示出来都是

- 无序列表
- 无序列表

怎么样，够简单吧……

### 4.3 `To do list`

通过无序列表我们还可以创建一个任务表（`To do list`），如下：

- [x] No.1
- [ ] No.2
- [x] No.3

语法如下：

```md
- [x] No.1
- [ ] No.2
- [x] No.3
```

其中 `[x]` 表示“已完成”，`[ ]` 表示“未完成”。可能`Hexo`有的时候渲染不出来这个，大家可以移步[原文件](https://github.com/Guleixibian2009/Website-Ariticle-Backup/blob/master/_posts/Markdown%E4%B8%ADLatex%E5%B8%B8%E7%94%A8%E8%AF%AD%E6%B3%95.md)查看！

### 4.4 合并列表

你可以把多种列表嵌套起来。如：

- Hello World!

- 这是一个列表……
  
  1. 里面还有一个列表！
  
  2. 的确是可以嵌套的！

- 还是原来那个列表\~
  
  - 可以同样嵌套无序列表
  
  - 等等等等
  
  - [x] 还可以更改列表类型啊！
  
  - [ ] 怎么样？

- 就是这样啦！

---

## 5.  文档里的小“零件”

### 5.1 分割线

分割线这个东东在文章分节这个功能上还是非常的实用的。你可以这样创建一条：

```markdown
---
或
***
```

正如你看到的那样啦！

### 5.2 强制换行的几种方式

在`Markdown`里面如果你不进行所谓强制换行，那么连续的段落就会被自动连接在一起。这个时候，`HTML`大兄就会来打杂：

```html
<br />
```

直接把它放在某一行的结尾，这两行就会自动拆分。如果你嫌麻烦...那么在想要换行的地方（行尾）加两个空格就可以......我也是没法展示了，这个不够直观。

### 5.3 符号的转义(`escaping`)

什么，这么简单的`Markdown`都需要转义？好吧，我承认，这还真的要！如果你仔细回想一下（或者预知一下未来，看下面的代码块）你就会发现，我们在处理文字样式的时候我们使用了各种符号，现整理如下：

| 符号   | 意义                    | 符号   | 意义                |
| ---- | --------------------- | ---- | ----------------- |
| `\`  | 反斜杠（转义本身）             | ``   | 反引号（代码块）          |
| `*`  | 星号（加粗，斜体，无序列表等）       | `_`  | 下划线（加粗，斜体等）       |
| `()` | 小括号（链接，图片）            | `[]` | 中括号（链接，图片）        |
| `~`  | 波浪号（下标，删除线）           | `$`  | 美元（某些情况下，`LaTex`） |
| `#`  | 井号（标题）                | `+`  | 加号（无序列表）          |
| `-`  | 减号（无序列表）              | `.`  | 点号（有序列表）          |
| `@`  | @号（`GFM`中，`@mention`） | `    | `                 |
| `<`  | 左尖括号（`HTML`）          | `>`  | 友尖括号（`HTML`）      |

那么，如何转义呢？只需要在需要转义的字符前面添加反斜杠就可以啦！比如，\*这段文字其实不是斜体\*！

代码如下：

```md
\*这段文字其实不是斜体!\*
*但这个是！*
```

### 5.4 没什么用的注释

```md
<!-- 这就是个注释了，我甚至不想讲… -->
```

对对，这就是个`HTML`注释而已。99.8%的情况下这个东东没有用，但如果…嗯好吧其实也不是一点作用都没有，如`Markdown`文档中的定位（比如你每天靠`GitHub Actions`生成点什么）或者`Hexo`文章的节选会使用`<!-- More -->`。

---

## 6. 激动人心！代码块

~~是不是等它好久了...~~ 行了也见了这么多行内代码块了，我怎么能不介绍一下呢。

行内代码块，只需将代码块内的内容用 ````包围起来就可以了。如，

```md
`hello, world!`
```

至于长篇的“大”代码块，有两种方法：

1. 在“代码块”前缩进4格，直到代码结束；

2. 使用下面这种方式：

<div class="highlight-container">
  <figure class="highlight md">
    <div class="table-container">
      <table>
        <tbody>
          <tr>
            <td class="gutter">
              <pre><span class="line">1</span>
<span class="line">2</span>
<span class="line">3</span></pre>
            </td>
            <td class="code">
              <pre><span class="line">```</span>
<span class="line">Here is some code.</span>
<span class="line">```</span></pre>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </figure>
  <div class="copy-btn"><i class="fa fa-clipboard fa-fw"></i></div>
</div>

想要指定语法并获得高亮技能？看到下面那个`python`没有！

<div class="highlight-container">
  <figure class="highlight md">
    <div class="table-container">
      <table>
        <tbody>
          <tr>
            <td class="gutter">
              <pre><span class="line">1</span>
<span class="line">2</span>
<span class="line">3</span>
<span class="line">4</span>
<span class="line">5</span>
<span class="line">6</span></pre>
            </td>
            <td class="code">
              <pre><span class="line">```python</span>
<span class="line">def hello():</span>
<span class="line">    print("Hello, world!")</span>
<span class="line"></span>
<span class="line">hello():</span>
<span class="line">```</span></pre>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </figure>
  <div class="copy-btn"><i class="fa fa-clipboard fa-fw"></i></div>
</div>

```python
def hello():
    print("Hello, world!")

hello()
```

## 7. 表格来了

需要在自己的文档中直观地表示数据？可以尝试列一个表格！Here we go\~

### 7.1 基本表格

|     | 第一列 | 第二列 | 第三列 |
| --- | --- | --- | --- |
| 第一行 | 数据1 | 数据2 | 数据3 |

光看这个表可能还真猜不出来它的语法是什么……但其实如果我真的写出来却会觉得这种语法也很直观！（不觉得那些竖线很像网格线吗）

```md
||第一列|第二列|第三列|
|第一行|数据1|数据2|数据3|
```

所以，每两个`|`之间是一格，5个`|`就是4格。没有限制最多多少行或多少列，且不要求每行格数相同！只是我这里渲染不出来……

### 7.2 每列的居中、靠右

什么，还有这种功能？好吧，我们只需要一条特殊“控制行”：

```md
|     | 第一列 | 第二列 | 第三列 |
| --- |:--- |:---:| ---:|
| 第一行 | 靠左  | 居中  | 靠右  |
```

|     | 第一列 | 第二列 | 第三列 |
| --- |:--- |:---:| ---:|
| 第一行 | 靠左  | 居中  | 靠右  |

---

到这里，你已经学完了基础的`Markdown`语法！想要学习`Markdown`中更高级的图表功能？敬请期待下一篇教程！

---

## 注释

以下是注释内容：  

[^1]: 你学废了吗？

___
