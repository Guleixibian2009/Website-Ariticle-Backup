---
title: Markdown中Latex常用语法
date: 2021-11-28 19:35:40
categories:
- [编程 , Markdown , LaTex]
tags:
- Markdown
- LaTex
- Maths
---

这篇文章是我<kbd>Ctrl+C</kbd><kbd>Ctrl+V</kbd>过来的，之后我还会再进行修改的，先凑活看着的吧......有些 $\LaTeX$标签可能显示不出来，同志们这是编译器的问题，因人而异......

## 0. LaTeX 是什么？

> $ \LaTeX $是一种基于`ΤeΧ`的排版系统，由美国计算机学家莱斯利·兰伯特（Leslie Lamport）在20世纪80年代初期开发.  
> 利用这种格式，即使使用者没有排版和程序设计的知识也可以充分发挥由`TeX`所提供的强大功能，能在几天、甚至几小时内生成很多具有书籍质量的印刷品。 
> 对于生成复杂表格和数学公式，这一点表现得尤为突出。因此它非常适用于生成高印刷质量的科技和数学类文档。这个系统同样适用于生成从简单的信件到完整书籍的所有其他种类的文档。

<!--more-->

### 0.1

文章中，标签以表格的形式呈现。**如果出现`/`的情况，代表某字符没有此形式。** *（如不存在`\varalpha`，这一格使用`/`填充）*

## 1. 希腊字母表

| Name       | Display    | Capital Case | Display    | Var Case      | Display       |
| ---------- |:----------:| ------------ |:----------:| ------------- |:-------------:|
| `\alpha`   | $\alpha$   | `\Alpha`     | $\Alpha$   | /             | /             |
| `\beta`    | $\beta$    | `\Beta`      | $\Beta$    | /             | /             |
| `\gamma`   | $\gamma$   | `\Gamma`     | $\Gamma$   | /             | /             |
| `\theta`   | $\theta$   | `\Theta`     | $\Theta$   | `\vartheta`   | $\vartheta$   |
| `\mu`      | $\mu$      | `\Mu`        | $\Mu$      | /             | /             |
| `\delta`   | $\delta$   | `\Delta`     | $\Delta$   | /             | /             |
| `\epsilon` | $\epsilon$ | `\Epsilon`   | $\Epsilon$ | `\varepsilon` | $\varepsilon$ |
| `\sigma`   | $\sigma$   | `\Sigma`     | $\Sigma$   | `\varsigma`   | $\varsigma$   |
| `\pi`      | $\pi$      | `\Pi`        | $\Pi$      | `\varpi`      | $\varpi$      |
| `\omega`   | $\omega$   | `\Omega`     | $\Omega$   | /             | /             |
| `\xi`      | $\xi$      | `\Xi`        | $\Xi$      | /             | /             |
| `\zeta`    | $\zeta$    | `\Zeta`      | $\Zeta$    | /             | /             |
| `\chi`     | $\chi$     | `\Chi`       | $\Chi$     | /             | /             |
| `\rho`     | $\rho$     | `\Rho`       | $\Rho$     | `\varrho`     | $\varrho$     |
| `\phi`     | $\phi$     | `\Phi`       | $\Phi$     | `\varphi`     | $\varphi$     |
| `\eta`     | $\eta$     | `\Eta`       | $\Eta$     | /             | /             |
| `\lambda`  | $\lambda$  | `\Lambda`    | $\Lambda$  | /             | /             |
| `\kappa`   | $\kappa$   | `\Kappa`     | $\Kappa$   | `\varkappa`   | $\varkappa$   |
| `\nu`      | $\nu$      | `\Nu`        | $\Nu$      | /             | /             |
| `\upsilon` | $\upsilon$ | `\Upsilon`   | $\Upsilon$ | /             | /             |
| `\psi`     | $\psi$     | `\Psi`       | $\Psi$     | /             | /             |
| `\tau`     | $\tau$     | `\Tau`       | $\Tau$     | /             | /             |
| `\iota`    | $\iota$    | `\Iota`      | $\Iota$    | /             | /             |

没有显示出来所有的字符？你可以尝试使用自己的编辑器来查看！

## 2.常用特殊字符表

### 2.1 数学符号类

| Name         | Display      | Name         | Display      | Name     | Display  | Name      | Display   |
| ------------ |:------------:| ------------ |:------------:| -------- |:--------:| --------- |:---------:|
| `\times`     | $\times$     | `\div`       | $\div$       | `\pm`    | $\pm$    | `\mp`     | $\mp$     |
| `\otimes`    | $\otimes$    | `\ominus`    | $\ominus$    | `\oplus` | $\oplus$ | `\odot`   | $\odot$   |
| `\oslash`    | $\oslash$    | `\triangleq` | $\triangleq$ | `\ne`    | $\ne$    | `\equiv`  | $\equiv$  |
| `\lt`        | $\lt$        | `\gt`        | $\gt$        | `\le`    | $\le$    | `\ge`     | $\ge$     |
| `\cup`       | $\cup$       | `\cap`       | $\cap$       | `\Cup`   | $\Cup$   | `\Cap`    | $\Cap$    |
| `\bigcup`    | $\bigcup$    | `\bigcap`    | $\bigcap$    | `\ast`   | $\ast$   | `\star`   | $\star$   |
| `\bigotimes` | $\bigotimes$ | `\bigoplus`  | $\bigoplus$  | `\circ`  | $\circ$  | `\bullet` | $\bullet$ |
| `\bigcirc`   | $\bigcirc$   | `\amalg`     | $\amalg$     | `\to`    | $\to$    | `\infty`  | $\infty$  |
| `\vee`       | $\vee$       | `\wedge`     | $\wedge$     | `\lhd`   | $\lhd$   | `\rhd`    | $\rhd$    |
| `\bigvee`    | $\bigvee$    | `\bigwedge`  | $\bigwedge$  | `\unlhd` | $\unlhd$ | `\unrhd`  | $\unrhd$  |
| `\sqcap`     | $\sqcap$     | `\sqcup`     | $\sqcup$     | `\prec`  | $\prec$  | `\succ`   | $\succ$   |
| `\subset`    | $\subset$    | `\supset`    | $\supset$    | `\sim`   | $\sim$   | `\approx` | $\approx$ |
| `\subseteq`  | $\subseteq$  | `\supseteq`  | $\supseteq$  | `\cong`  | $\cong$  | `\doteq`  | $\doteq$  |
| `\setminus`  | $\setminus$  | `\mid`       | $\mid$       | `\ll`    | $\ll$    | `\gg`     | $\gg$     |
| `\parallel`  | $\parallel$  | `\Join`      | $\Join$      | `\in`    | $\in$    | `\notin`  | $\notin$  |
| `\propto`    | $\propto$    | `\neg`       | $\neg$       | `\ldots` | $\ldots$ | `\cdots`  | $\cdots$  |
| `\forall`    | $\forall$    | `\exists`    | $\exists$    | `\vdots` | $\vdots$ | `\ddots`  | $\ddots$  |
| `\aleph`     | $\aleph$     | `\nabla`     | $\nabla$     | `\imath` | $\imath$ | `\jmath`  | $\jmath$  |
| `\ell`       | $\ell$       | `\partial`   | $\partial$   | `\int`   | $\int$   | `\oint`   | $\oint$   |
| `\uplus`     | $\uplus$     | `\biguplus`  | $\biguplus$  | /        | /        | /         | /         |

### 2.2 箭头类

| Name                 | Display              | Name                  | Display               |
| -------------------- |:--------------------:| --------------------- |:---------------------:|
| `\triangleleft`      | $\triangleleft$      | `\triangleright`      | $\triangleright$      |
| `\bigtriangleup`     | $\bigtriangleup$     | `\bigtriangledown`    | $\bigtriangledown$    |
| `\uparrow`           | $\uparrow$           | `\downarrow`          | $\downarrow$          |
| `\leftarrow`         | $\leftarrow$         | `\rightarrow`         | $\rightarrow$         |
| `\Leftarrow`         | $\Leftarrow$         | `\Rightarrow`         | $\Rightarrow$         |
| `\longleftarrow`     | $\longleftarrow$     | `\longrightarrow`     | $\longrightarrow$     |
| `\Longleftarrow`     | $\Longleftarrow$     | `\Longrightarrow`     | $\Longrightarrow$     |
| `\leftrightarrow`    | $\leftrightarrow$    | `\longleftrightarrow` | $\longleftrightarrow$ |
| `\Leftrightarrow`    | $\Leftrightarrow$    | `\Longleftrightarrow` | $\Longleftrightarrow$ |
| `\leftharpoonup`     | $\leftharpoonup$     | `\rightharpoonup`     | $\rightharpoonup$     |
| `\leftharpoondown`   | $\leftharpoondown$   | `\rightharpoondown`   | $\rightharpoondown$   |
| `\rightleftharpoons` | $\rightleftharpoons$ | `\S`                  | $\S$                  |
| `\nwarrow`           | $\nwarrow$           | `\nearrow`            | $\nearrow$            |
| `\swarrow`           | $\swarrow$           | `\searrow`            | $\searrow$            |
| `\triangle`          | $\triangle$          | `\box`                | $\Box$                |
| `\diamond`           | $\diamond$           | `\diamondsuit`        | $\diamondsuit$        |
| `\heartsuit`         | $\heartsuit$         | `\clubsuit`           | $\clubsuit$           |
| `\spadesuit`         | $\spadesuit$         | /                     | /                     |

## 3. 公式语法

1. 上下标`_{下标}^{上标}`：  

| 语法                | 输出                    |
|:-----------------:|:---------------------:|
| `y = x_i^{a_1^2}` | $$ y = x_i^{a_1^2} $$ |

2. 公式中插入文本（直接上）：

| 语法                  | 输出                     |
|:-------------------:|:----------------------:|
| `y = x^2 \; (二次函数)` | $ y = x^{2} \; (二次函数)$ |

3. 公式中插入空格`\,` `\;` `\quad` `\qquad`间隔依次变宽：

| 语法           | 输出           |
|:------------:|:------------:|
| `ab`         | $ab$         |
| `a \, b`     | $a \, b$     |
| `a \; b`     | $a \; b$     |
| `a \quad b`  | $a \quad b$  |
| `a \qquad b` | $a \qquad b$ |

4. 字母上方横线`\overline{}`,`\bar{}`：

| 语法               | 输出               |
|:----------------:|:----------------:|
| `\overline{ABC}` | $\overline{ABC}$ |
| `\bar{A}`        | $\bar{A}$        |

5. 字母下方横线`\underline{}`：

| 语法                | 输出                |
|:-----------------:|:-----------------:|
| `\underline{ABC}` | $\underline{ABC}$ |

6. 字母上方波浪线`\tilde{}`, `\widetilde{}`：

| 语法                  | 输出                  |
|:-------------------:|:-------------------:|
| `\tilde{\rho}`      | $\tilde{\rho}$      |
| `\widetilde{A1B2C}` | $\widetilde{A1B2C}$ |

7. 字母上方尖号`\hat{}, \widehat{}`：

| 语法              | 输出              |
|:---------------:|:---------------:|
| `\hat{A}`       | $\hat{A}$       |
| `\widehat{ABC}` | $\widehat{ABC}$ |

8. 字母上方箭头`\vec{}, \overleftarrow{}, \overrightarrow{}`：

| 语法                    | 输出                    |
|:---------------------:|:---------------------:|
| `\vec{ab}`            | $\vec{ab}$            |
| `\overleftarrow{ab}`  | $\overleftarrow{ab}$  |
| `\overrightarrow{ab}` | $\overrightarrow{ab}$ |

9. 字母上方花括号`\overbrace{}`，或下方花括号`\underbrace{}`：
    $ \overbrace{1+2+3} \mbox{ 或 } \underbrace{1+2+3} $
- 字母上方点号`\dot{}, \ddot{}`：
    $ \dot{a} \mbox{ 或 } \ddot{a} $

- 省略号`\dots, \cdots`
    $ 1,2,\dots  \qquad  1,2,\cdots $

- 积分`\int_{}^{}`：  
    $ \int_{-\infty}^{+\infty} f(x) \mathrm{d}x $  ​
  
    双重积分`\iint`：$ \iint_{-\infty}^{+\infty} f(x,y) \mathrm{d}x \mathrm{d}y $ 
    行内积分：$$nt_{-\infty}^{+\infty} f(x) \mathrm{d}x$$$  行内积分limits模式`\int\limits_{}^{}`：$$\$\limits_{-\infty}^{+\infty} f(x) \mathrm{d}x$$  $行内积分display模式`\displaystyle \int_{}^{}`：  $$\displaystyle \int_{-\infty}^{+\infty} f(x) \mathrm{d}x$$​​​ $​  
  
    圆圈积分`\oint`：$ \oint_{-\infty}^{+\infty} $​    

- 求和`\sum_{}^{}`：  
    $ \sum_{i=1}^{n} i^2 $​​    
  
    行内求和：$\sum_{i=1}^{n} i^2$ 
    行内求和limits模式`\sum\limits_{}^{}`：$$um\limits_{i=1}^{n} i^2$$$  行内求和display模式`\displaystyle \sum_{}^{}`：  $$\$playstyle \sum_{i=1}^{n} i^2$$​​$​​  

- 求乘积`\prod_{}^{}`：  
    $ \prod_{i=1}^{n} a_i $

- 分数`\frac{up}{down}`：
    $ x_1,x_2 = \frac{b^2 \pm 4ac}{2a} $

- 根号`\sqrt`：
    $ r = \sqrt{x^2+y^2} $
  
    多次根号`\sqrt[n]`：   
  
    $ x^{2/3} = \sqrt[3]{x^2} $

## 4. 方程组

- 左侧花括号
  
  ```latex
  \begin{equation}
  \left\{ 
  \begin{aligned}
  \min \quad&{f=a-b}\ \
  {s.t.}\quad &{a =b(x), \quad x\in [0,L] } \ \
  (c+d)(e+f)=e \ \
  (df+cg)=0 \ \
  (adv-ert)(e+f)=e
  \end{aligned} \right.
  \end{equation}
  ```
  
  注意：在 markdown 环境下，某些特殊字符，如'\', '\*'等，会首先被 markdown 语法转义，然后再被 Latex 转义。
  因此有时候 '\{'需要写作'\\{'，'\*'需要写作'\\*'，'\\'需要写作'\\\\'等，视不同的解释环境而定

```
  **注**：如果各个方程需要在某个字符处对齐（如等号对齐），只需在所有要对齐的字符前加上 `&` 符号。如果不需要公式编号，只需在宏包名称后加上 `*` 号。

$$
\begin{equation}
\left\{ 
\begin{aligned}
\min \quad&{f=a-b}\\
{s.t.}\quad &{a =b(x), \quad x\in [0,L] } \\
(c+d)(e+f)&=e \\
(df+cg)&=0 \\
(adv-ert)(e+f)&=e
\end{aligned} \right.
\end{equation}
$$
```

$$
\begin{equation}
\left\{ 
\begin{aligned}
\min \ &{f=a-b}\\
{s.t.}\  &{a =b(x), \quad x\in [0,L] } \\
(c+d)(e+f)&=e \\
(df+cg)&=0 \\
(adv-ert)(e+f)&=e
\end{aligned} \right.
\end{equation}
$$

- 分情况讨论方程式

```latex
f(x) =
\begin{cases}
x^2 \qquad & a \gt 0 \\
e^x \qquad & a \le 0
\end{cases}
```

$$
f(x) = \begin{cases}
x^2 \qquad & a \gt 0 \\
e^x \qquad & a \le 0
\end{cases}
$$