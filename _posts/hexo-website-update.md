---
title: Hexo深度个性化——底层配置
date: 2023-01-01 16:25:40
tags:
- CSS
- Frontend
- HTML
- Hexo
- JavaScript
- Website
categories:
- [GitHub, Pages, Hexo]
---

新年伊始，没想到，我又决定回来更新了。这是我之前就想好的题目，今天终于动笔——`Hexo`博客的深度个性化。（不瞒着你们，我一向这样，更一段时间，鸽一段时间。也许看着这学期我周更，但那些都是一些感想，并不是特别花时间的技术博）

这里会讲一讲：

1. `back2top`按钮百分比的动画还有进度条颜色

2. 相关文章推荐模块中的`CSS`统一

3. 给个别文章添加`Creative Commons`许可证开关

4. 主页文章节选悬浮特效

<!--more-->

## 1. 关于阅读百分比

![](https://s1.ax1x.com/2023/01/01/pSCf3HU.png)

可以看到我这个博客之前既启用了顶部进度条和`back2top`里的百分比，我个人觉得有点重复，想要把百分比数字只在鼠标悬浮时显示，并且给它加个动画。进度条的颜色光绿色也有点单调，我想加一个蓝-绿色渐变。这个都是可以通过`CSS`实现的，在`Hexo`中则是`stylus`。

在`Hexo`中想要改`CSS`的话，先别急着去新建文件，最好先在`themes/next/source/css`这个文件夹里面找一找，阅读百分比的两个文件在`_common/components`文件夹里。

### 1.1 阅读百分比动画

要实现这个我首先的思路就是给`width`加`transition`，再配合`overflow: hidden`来实现；不过为了如此我们要给这个元素加一点额外的属性。

![](https://s1.ax1x.com/2023/01/02/pSPFnPg.png)

这个百分比是`div#back-to-top`里面的一个`span`，对应的`stylus`是`back-to-top.styl`。

```stylus
.back-to-top {
  background: $b2t-bg-color;
  bottom: $b2t-position-bottom;
  box-sizing: border-box;
  color: $b2t-color;
  cursor: pointer;
  left: $b2t-position-right;
  opacity: $b2t-opacity;
  position: fixed;
  transition-property: bottom;
  z-index: $zindex-3;

  if (hexo-config('back2top.scrollpercent')) {
    width: initial;
  } else {
    width: 24px;

    span {
      display: none;
    }
  }

  &:hover {
    color: $sidebar-highlight;
  }

  &.back-to-top-on {
    bottom: $b2t-position-bottom-on;
  }

  +tablet-mobile() {
    left: $b2t-position-right-mobile;
    opacity: $b2t-opacity-hover;
  }

}
```

这里有两个注意点：

1. `transition`要求`width`必须是定值，不能是`auto`，故我们要手动去加一个`width`和`padding`，以保证美观。

2. 能应用`width`属性说明这个`<span>`的`display`至少要是`inline-block`，不能是`inline`。

综合我一开始的想法并结合这两个要点，这里给出最终代码：

```stylus
.back-to-top {
  background: $b2t-bg-color;
  bottom: $b2t-position-bottom;
  box-sizing: border-box;
  color: $b2t-color;
  cursor: pointer;
  left: $b2t-position-right;
  opacity: $b2t-opacity;
  padding: 0 3px 0 6px;
  position: fixed;
  transition-property: bottom;
  z-index: $zindex-3;

  if (hexo-config('back2top.scrollpercent')) {
    width: initial;
  } else {
    width: 24px;

    span {
      display: none;
    }
  }

  &:hover {
    color: $sidebar-highlight;
    padding: 0 6px;

    span {
      width: 32px;
    }
  }

  &.back-to-top-on {
    bottom: $b2t-position-bottom-on;
  }

  +tablet-mobile() {
    left: $b2t-position-right-mobile;
    opacity: $b2t-opacity-hover;
  }

  span {
    height: 12px;
    line-height: 15px;
    overflow: hidden;
    display: inline-block;
    width: 0;
    transition-property: width;
    transition-duration: 0.5s;
  }

}
```

### 1.2 阅读进度条渐变色

在我们的主题配置文件中，这一块是用来配置进度条的。

![](https://s1.ax1x.com/2023/01/02/pSPFeIS.png)

```yml
# Reading progress bar
reading_progress:
  enable: true
  # Available values: top | bottom
  position: top
  color: "#37c6c0"
  height: 3px
```

这个`color`属性就是用来调颜色的。然而如果是渐变的话，就一定要用`linear-gradient()`，对应的`CSS`属性则是`background-image`。以防万一，我去看了一下`themes/next/source/css/_common/components/reading-progress.styl`，里面对应一行是：

```stylus
background: unquote(hexo-config('reading_progress.color'))
```

它用的是通用的`background`，这样就万无一失了。我们直接把`color`改成：

```yml
color: "linear-gradient(to right, #2299dd , #37c6c0)"
```

并重新生成即可。

![](https://s1.ax1x.com/2023/01/02/pSPFuGQ.png)

***

## 2. 相关文章推荐中的`CSS`统一

如果你像我之前一样，安装了相关文章推荐模块，却不对其进行任何调整，你会收获这样的文章推荐：

![](https://s1.ax1x.com/2023/01/01/pSCfY4J.png)

![](https://s1.ax1x.com/2023/01/01/pSCfGEF.png)

字号、行距不统一，粗体、斜体没消除，甚至还有图片，根本不像一份合格的文章节选。原因在于，这个相关文章模块和文章主体共用`CSS`。我们要做的，就是用`!important`覆盖掉。

![](https://s1.ax1x.com/2023/01/02/pSPmQtP.png)

这个节选是`div.popular-posts-excerpt`，默认继承`main.css`中的样式。找一下对应的`stylus`文件，是`themes/next/source/css/_common/components/third-party/related-posts.styl`。我们直接在末尾添加一段

```stylus
.popular-posts-excerpt{ 
  p, strong, i, a, h1, h2, h3, h4, h5, h6 {
    text-decoration: none !important;
    font-weight: normal !important;
    font-style: normal !important;
    font-size: 0.875em !important;
    margin: 0 0 0 0;

    br {
      display: none;
    }
  }

  img {
    display: none !important;
  }
}
```

就可以规避掉大部分问题。后续如果发现更多需要屏蔽或调整的，也直接加在这里就好了。

***

## 3. 给文章内`Creative Commons`加个开关

![](https://s1.ax1x.com/2023/01/01/pSCfJN4.png)

在技术博中，转载和引用是常有的事。然而`Next`自带的版权方框就是这么尴尬，默认是串联起来的，只能在主题配置文件中选择全开或全关。全开时，不是你写的硬要说成你写的，心里总是不安。

不过，有一种办法是类似之前我们有一个文章开头`yml`里配置的属性，叫做`sticky`。我们可以做一个类似的开关，比如叫`nocopyright`，`true`代表转载，不会显示版权方框；`false`或不写，则会显示。于是乎我们去看一下版权方框的生成逻辑，在`themes/next/layout/_macro`里的`post.swig`里面，大约在225行：

```nunjucks
{%- if theme.creative_commons.license and theme.creative_commons.post %}
  {{ partial('_partials/post/post-copyright.swig') }}
{%- endif %}
```

这是`Nunjucks`中的一个简单的条件语句，我们只要添加一个条件`and not page.nocopyright`就可以了。`page`指的是当前渲染的文章。所以就是这样：

```nunjucks
{%- if theme.creative_commons.license and theme.creative_commons.post and not page.nocopyright %}
  {{ partial('_partials/post/post-copyright.swig') }}
{%- endif %}
```

然后找到你不想显示版权方框的文章，在开头的`YAML Front Matter`里面加一行：

```yml
nocopyright: true
```

即可。需要显示则不需要加，默认显示。

***

## 4. 主页文章悬浮特效

这个的话，我主要是想做一个缩放+透明度的`transition`，应用在主页的`article.post-block`上面。不过我特意去检查了一下，在文章页也有这样的元素，但我只希望对主页应用，所以我找到一个父类`index`（文章内则是`post`）。

![](https://s1.ax1x.com/2023/01/02/pSPdKfS.png)

这个就是简单的`CSS`了，随便找一段`styl`插进去，我就加在了`themes/next/source/css/_common/components/post/post-expand.styl`里面了：

```stylus
.index {
  article.post-block {
    background-color: rgba(255, 255, 255, 1) !important
    transform: scale(1);
    transition: transform 0.5s, background-color 0.5s;
  }

  article.post-block:hover {
    background-color: rgba(255, 255, 255, 0.4) !important
    transform: scale(1.012);
    transition: transform 0.5s, background-color 0.5s;
  }
}
```

这样就能实现缩放+透明度的特效了。

***

总的来说，`Hexo+Next`留给个人的发挥空间还是非常大的，底层逻辑完全开放且容易修改，因此个性化变得非常简单，只需要一点点`CSS`的知识就能让你的博客锦上添花！

**THE END**感谢您的阅读\~
