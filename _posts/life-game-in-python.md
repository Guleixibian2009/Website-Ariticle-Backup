---
title: 生命游戏：在不确定中寻找确定
date: 2023-01-08 08:02:11
tags:
- Python
- 编程
categories:
- [编程, Python]
---

“在不确定中寻找确定”，这是我的语文老师在2022年2月刚开始转线上课时对我们的一句嘱咐。如今，疫情尘埃落定，也据说再也不会有网课了。也许，这就是生命——不断前行、变幻莫测。

但这两个词，又让我想起了另一种“生命”——康威生命游戏。这两天，灵机一动，我用`Python`实现了这“零玩家游戏”。

<!--more-->

## 1. 生命游戏——变化与生死

最早接触到生命游戏是在为[漫谈密码学](../../../../2023/01/06/ramble-on-cryptography/)这个项目找资料时，看到一个视频[数学有一个致命的缺陷](https://www.bilibili.com/video/BV1464y1k7Ya/)——就是在那篇文章中的最后一个视频。这个视频的开头提到了康威和他的生命游戏。视频里说，虽然生命游戏只有这么短短几条规则，却可以无限地繁衍下去，没有人知道是会无限进行、陷入循环还是直接停止。这充满“变化与生死”的“零玩家”游戏的规则如下：

首先，我们有一个网格，理论上无穷大，这里我们就`20x20`。这个网格的每一个格子代表一个细胞，并拥有两种状态——白色为生，黑色为死。网格上细胞的状态是随机生成的，之后会按照一个特定的判断方法来决定这个细胞是生是死：

1. 当这个细胞为死，如果在自己周围一圈正好有3个活细胞，自己在下一次更新时就会变为活——模拟繁衍

2. 当这个细胞为活：
   
   1. 如果周围有多于3个活细胞，下一轮就会死——模拟生命过多
   
   2. 如果周围刚好有2或3个活细胞，下一轮还是为活
   
   3. 如果周围少于2个活细胞，下一轮就会死——模拟生命过少

总结出来就是这样：

1. 如果在自己周围一圈正好有3个活细胞，下一轮一定为活

2. 如果周围刚好有2个活细胞，下一轮保持原样

3. 其他时候，下一轮为死。

遵循这个规则，网格上的细胞就可以开始繁殖了。

![](https://s1.ax1x.com/2023/01/08/pSZV6ij.png)

****

## 2. 生命游戏——规则与破坏

### 2.1 静物

多运行几轮之后，你会发现，在生命游戏中，有那么几种结构，只要没有外力破坏，就可以保持稳定。例如：

![](https://s1.ax1x.com/2023/01/08/pSZVcJs.png)

人们根据其形状，给其中一些结构起了名字，例如`2x2`方块等：

![](https://s1.ax1x.com/2023/01/08/pSZV2zq.png)

### 2.2 振荡器

还有一部分结构，虽然不稳定，但它们的变化有一定的规律。比如说：一个长度为3的横——“闪光灯”：

![](https://s1.ax1x.com/2023/01/08/pSZVsoQ.png)

### 2.3 飞船

此外，最有意思的一种结构，叫做飞船。它们的变化也有规律，但每完成一个周期，它们都会定向移动一段距离。其中运动最快的周期为4，叫做滑翔机：

![](https://s1.ax1x.com/2023/01/08/pSZVWQ0.png)

---

## 3. `Python`模拟生命游戏

```python
import tkinter as tk
import random, time

def inRange(n, start, end = 0):
    return start <= n <= end if end >= start else end <= n <= start

root = tk.Tk()
root.title("Life")
root.geometry("600x600")
canvas = tk.Canvas(root,width=600,height=600,bg='black')
canvas.pack()
```

首先我们进行一个初始化，创建`root`和`canvas`。这里还用到了以前定义过的`inRange`函数。

```python
class Game:
    def __init__(self):
        life_list = []
        for x in range(60):
            newList = []
            for y in range(60):
                newList.append(random.choice([0,1]))
            life_list.append(newList)


        new_life_list = []
        for x in range(60):
            newList = []
            for y in range(60):
                newList.append(0)
            new_life_list.append(newList)
        self.running = 1
        self.root = root
        self.canvas = canvas
        self.life_list = life_list
        self.new_life_list = new_life_list

        self.canvas.bind("<Button-1>",self.mouseUpdate)
```

然后的话我们定义一个`Game`类，这里面有两个二维数组`life_list`和`new_life_list`，以便我们后面计算。为了不把原先的图和新计算的图搞混，我们需要两个列表来完成计算。

```python
        for x in range(1,59):
            for y in range(1,59):
                if self.life_list[x][y]:
                    self.canvas.create_rectangle(10*x,10*y,10*x+10,10*y+10,fill="white")
                else:
                    self.canvas.create_rectangle(10*x,10*y,10*x+10,10*y+10,fill="black")
```

这个是一个绘制程序。为了避免边界情况，我们不绘制/计算边界。

```python
def update(self):
        for x in range(1,59):
            for y in range(1,59):
                around = self.life_list[x-1][y-1]+self.life_list[x-1][y]+self.life_list[x-1][y+1]+self.life_list[x][y-1]+self.life_list[x][y+1]+self.life_list[x+1][y-1]+self.life_list[x+1][y]+self.life_list[x+1][y+1]
                if around == 3:
                    self.new_life_list[x][y] = 1
                elif around == 2:
                    self.new_life_list[x][y] = self.life_list[x][y]
                else:
                    self.new_life_list[x][y] = 0

        for x in range(1,59):
            for y in range(1,59):
                if self.new_life_list[x][y]:
                    self.canvas.create_rectangle(10*x,10*y,10*x+10,10*y+10,fill="white")
                else:
                    self.canvas.create_rectangle(10*x,10*y,10*x+10,10*y+10,fill="black")
        self.life_list = self.new_life_list
        self.new_life_list = []
        for x in range(60):
            newList = []
            for y in range(60):
                newList.append(0)
            self.new_life_list.append(newList)
```

随后的话这是一个更新函数，按照我们已定义的规则`Birth 3 / Survive 23`（对之前规则的一种官方缩写）来计算新一轮`life_list`。因为我们是用1和0来带表生和死，所以我们可以通过计算8个格子的和来求周围格子的情况。

然后我们重新绘制，并重置`new_life_list`，来为下一次计算做准备。

```python
    def mouseUpdate(self,event):
        for x in range(1,59):
            for y in range(1,59):
                around = self.life_list[x-1][y-1]+self.life_list[x-1][y]+self.life_list[x-1][y+1]+self.life_list[x][y-1]+self.life_list[x][y+1]+self.life_list[x+1][y-1]+self.life_list[x+1][y]+self.life_list[x+1][y+1]
                if around == 3:
                    self.new_life_list[x][y] = 1
                elif around == 2:
                    self.new_life_list[x][y] = self.life_list[x][y]
                else:
                    self.new_life_list[x][y] = 0

        cellX = int(event.x / 10)
        cellY = int(event.y / 10)
        if inRange(cellX, 1, 59) and inRange(cellY, 1, 59):
            self.new_life_list[cellX][cellY] = 1

        for x in range(1,59):
            for y in range(1,59):
                if self.new_life_list[x][y]:
                    self.canvas.create_rectangle(10*x,10*y,10*x+10,10*y+10,fill="white")
                else:
                    self.canvas.create_rectangle(10*x,10*y,10*x+10,10*y+10,fill="black")
        self.life_list = self.new_life_list
        self.new_life_list = []
        for x in range(60):
            newList = []
            for y in range(60):
                newList.append(0)
            self.new_life_list.append(newList)
```

这里是对鼠标事件的支持。因为我们在`__init__()`中绑定过鼠标左键，所以点击时我们能知道鼠标的坐标，除以10就是对应的格子——这里还是避免掉边界情况。

```python
    def mainloop(self):
        self.update()
        self.root.update()
        time.sleep(0.1)
        self.canvas.delete("all")
```

然后调用`update`函数，更新页面，等待0.1秒后清除页面（释放内存，提高运行速度）

```python
g = Game()
def allStop():
    try:
        g.root.destroy()
        btnRoot.destroy()
    except:
        btnRoot.destroy()
def nonstop():
    g.__init__()
    g.running = 1
    while g.running:
        g.mainloop()
def stop():
    g.running = 0
    g.update()

btnRoot = tk.Tk()
btn1 = tk.Button(btnRoot, text="Start Random Nonstop",command=nonstop)
btn1.pack()
btn2 = tk.Button(btnRoot, text="Stop Random Nonstop",command=stop)
btn2.pack()
btnRoot.protocol("WM_DELETE_WINDOW", allStop)
btnRoot.mainloop()
```

最后就是绘制一些功能按钮、定义功能函数了。`nonstop()`函数中重复调用`g.__init__()`是为了随机生成新的图像。

完整代码如下：

```python
import tkinter as tk
import random, time

def inRange(n, start, end = 0):
    return start <= n <= end if end >= start else end <= n <= start

root = tk.Tk()
root.title("Life")
root.geometry("600x600")
canvas = tk.Canvas(root,width=600,height=600,bg='black')
canvas.pack()

class Game:
    def __init__(self):
        life_list = []
        for x in range(60):
            newList = []
            for y in range(60):
                newList.append(random.choice([0,1]))
            life_list.append(newList)


        new_life_list = []
        for x in range(60):
            newList = []
            for y in range(60):
                newList.append(0)
            new_life_list.append(newList)
        self.running = 1
        self.root = root
        self.canvas = canvas
        self.life_list = life_list
        self.new_life_list = new_life_list

        self.canvas.bind("<Button-1>",self.mouseUpdate)

        for x in range(1,59):
            for y in range(1,59):
                if self.life_list[x][y]:
                    self.canvas.create_rectangle(10*x,10*y,10*x+10,10*y+10,fill="white")
                else:
                    self.canvas.create_rectangle(10*x,10*y,10*x+10,10*y+10,fill="black")

    def mouseUpdate(self,event):
        for x in range(1,59):
            for y in range(1,59):
                around = self.life_list[x-1][y-1]+self.life_list[x-1][y]+self.life_list[x-1][y+1]+self.life_list[x][y-1]+self.life_list[x][y+1]+self.life_list[x+1][y-1]+self.life_list[x+1][y]+self.life_list[x+1][y+1]
                if around == 3:
                    self.new_life_list[x][y] = 1
                elif around == 2:
                    self.new_life_list[x][y] = self.life_list[x][y]
                else:
                    self.new_life_list[x][y] = 0

        cellX = int(event.x / 10)
        cellY = int(event.y / 10)
        if inRange(cellX, 1, 59) and inRange(cellY, 1, 59):
            self.new_life_list[cellX][cellY] = 1

        for x in range(1,59):
            for y in range(1,59):
                if self.new_life_list[x][y]:
                    self.canvas.create_rectangle(10*x,10*y,10*x+10,10*y+10,fill="white")
                else:
                    self.canvas.create_rectangle(10*x,10*y,10*x+10,10*y+10,fill="black")
        self.life_list = self.new_life_list
        self.new_life_list = []
        for x in range(60):
            newList = []
            for y in range(60):
                newList.append(0)
            self.new_life_list.append(newList)

    def update(self):
        for x in range(1,59):
            for y in range(1,59):
                around = self.life_list[x-1][y-1]+self.life_list[x-1][y]+self.life_list[x-1][y+1]+self.life_list[x][y-1]+self.life_list[x][y+1]+self.life_list[x+1][y-1]+self.life_list[x+1][y]+self.life_list[x+1][y+1]
                if around == 3:
                    self.new_life_list[x][y] = 1
                elif around == 2:
                    self.new_life_list[x][y] = self.life_list[x][y]
                else:
                    self.new_life_list[x][y] = 0

        for x in range(1,59):
            for y in range(1,59):
                if self.new_life_list[x][y]:
                    self.canvas.create_rectangle(10*x,10*y,10*x+10,10*y+10,fill="white")
                else:
                    self.canvas.create_rectangle(10*x,10*y,10*x+10,10*y+10,fill="black")
        self.life_list = self.new_life_list
        self.new_life_list = []
        for x in range(60):
            newList = []
            for y in range(60):
                newList.append(0)
            self.new_life_list.append(newList)


    def mainloop(self):
        self.update()
        self.root.update()
        time.sleep(0.1)
        self.canvas.delete("all")


g = Game()
def allStop():
    try:
        g.root.destroy()
        btnRoot.destroy()
    except:
        btnRoot.destroy()
def nonstop():
    g.__init__()
    g.running = 1
    while g.running:
        g.mainloop()
def stop():
    g.running = 0
    g.update()

btnRoot = tk.Tk()
btn1 = tk.Button(btnRoot, text="Start Random Nonstop",command=nonstop)
btn1.pack()
btn2 = tk.Button(btnRoot, text="Stop Random Nonstop",command=stop)
btn2.pack()
btnRoot.protocol("WM_DELETE_WINDOW", allStop)
btnRoot.mainloop()   
```

***

想来也许，我们这个宇宙也就是一个放大版的生命游戏，只要几条基础物理定律，就可以发展成整个宇宙。

**THE END**感谢您的阅读\~
