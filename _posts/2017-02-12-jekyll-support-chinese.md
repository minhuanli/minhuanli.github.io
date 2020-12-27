---
layout: post
title: Jekyll博客的中文支持
description: 尝试在Jekyll博客中使用多种语言，包括在CSS样式表中更改博客不同内容的中文字体，同时保持英文字体的统一性。<br>Add support of Chinese language to Jekyll blog. CSS stylesheet is configured to use different Chinese font for different sections, while keeping consistent English font.
tags: jekyll blog chinese multilingual font github-page
lang: zh
---


<style>
.highlight-left {margin-left: 0}
</style>

你好，世界！

这是我的第一篇中文博客。经过几个小时的调试，我终于搞定了Jekyll模板下的中文支持。这篇文章就是一个例子。我将在这篇博客中介绍具体的实现步骤。

Jekyll是一个静态网站生成器，它可以很方便得在服务器上部署。如果你有自己的服务器空间，那么网上搜到不少Jekyll的多语言插件，直接使用那些插件会比这篇文章介绍的方法简单得多。但是，如果你像我一样倾向于使用Github Pages提供的个人博客空间，这些语言支持的插件都是完全不可用的。我们需要的是一个不依赖于任何插件的解决方案。

### 效果展示

首先，我先展示一下Jekyll博客的各种功能，在使用中文时的样式：

#### 1. 引用框

> 苟利国家生死以，岂因祸福避趋之。<br>
One should uphold his country’s interest with his life, he should not do things just to pursue his personal gains and he should not be evade responsibilities for fear of personal loss.

引用框中的中文使用楷体，英文使用原本的英文字体。

#### 2. 代码框

```python
# Python code snippet
print("Hello World!")
```

由于代码一般是英文的，所以代码框沿用整体的英文字体。

#### 3. 超链接

* [我的博客主页](http://longqian.me)
* [我的个人信息主页](http://longqian.me/aboutme)
* [我的Github主页](https://github.com/qian256)


### 实现方法

#### 1. 区别中文和英文的页面

首先，我们需要告诉Jekyll那些博客是中文，哪些是英文，这样做的好处是能够把这两类文章的格式分开处理。当然，在中文博客中是兼容英文的。我们只需要在每篇中文的博客的front matter区域注明它的语言是中文，例如这篇文章的front matter是这样的：

```
---
layout: post
title: Jekyll博客的中文支持
description: blablablabla
tags: jekyll blog chinese multilingual font github-page
lang: zh
---
```

我们给这个网页增加了一个变量`page.lang = zh`。在需要对中文分别处理的地方，检测这个变量是否存在即可判断所用语言不同。

#### 2. 区别渲染中英文的页面

HTML的标准中有一个变量`lang`，用来指定该HTML元素的语言。例如：

```html
<p lang="fr">Ceci est un paragraphe.</p>
```

制定了这个段落的语言是法语。那么对于特定的语言，我们可以控制CSS样式表来区别对待。例如：

```css
p {font-size: 2rem;}
p:lang(fr) {font-size: 3rem;}
```

就可以把法语的段落字体放大。

Jekyll主要有两种页面：page和post。另外，,对于这两种页面，如果被指定为中文，我们将这个页面的HTML的语言变量设置为`page.lang`的内容。我们需要修改`_layouts/page.html`和`_layouts/post.html`，例如：

{% highlight html %}{% raw %}
{% if page.lang %}
<div class="post" lang="{{page.lang}}">
{% else %}
<div class="post">
{% endif %}
  ACTUAL CONTENT HERE
</div>
{% endraw %}{% endhighlight %}{: .highlight-left }

以上代码实现了对中英文post页面的HTML`lang`变量的设置。对page页面以及index页面需要同样的操作。如果你的博客有tagpage的话，tagpage中相应的page也需要设置`lang`变量。

#### 3. 中文字体

在修改CSS样式表之前，我们先准备所需的中文字体。考虑到对于不同浏览器和操作系统的统一，我并不倾向于使用系统字体，而是把字体也存放在我的服务器上。我的中文字体是从[Google Font Noto](https://www.google.com/get/noto/)中下载的。虽然Google Font目前的中文字体不多，不过暂时能够满足我博客的需求。我下载了黑体（用于正文），楷体（用于引用段落）和明体（用于标题）。

只需要在`_includes/head.html`中加入保存的字体样式表即可：

```css
<link rel="stylesheet" href="/PATH/TO/CHINESE/FONTS.css">
```


#### 4. 不同区域的显示样式

基于第2步中的基本规则，我们需要对不同HTML区域采用不同的样式。以我的博客为例：

```css
h1, h2, h1 a, h2 a:lang(zh) {
  font-family: "PT Sans", "cwTeXMing", serif;
}
h3, h4, h5, h6, p, table, img, a:lang(zh) {
  font-family: "PT Sans", "Noto Sans SC", "Microsoft YaHei", sans-serif;
}
blockquote p:lang(zh){
  font-family: "PT Sans", "STKaiti", "Kaiti", "cwTeXKai", "Microsoft YaHei", sans-serif;
}
```

将`"PT Sans"`放在第一位使得中文页面中的英文字体得以保留。

#### 5. 细节调试

多语言支持涉及到页面中的各种HTML元素及其摆列组合，很容易有所疏漏。建议在本地编译后仔细查看一番。

#### 6. 上传到Github或者服务器



### 最后

如果需要更多语言的支持，可以在front matter添加其他语言项目，例如:`fr`或者`jp`。与之对应的，下载相应语言的字体，修改CSS样式即可。

中文的技术资源和英文的技术资源几乎是两个平行世界。网上也鲜有在英文Jekyll模板中添加中文语言支持的例子。希望这篇文章对你有所帮助！

感谢阅读！  <i class="em em-lq"></i>
