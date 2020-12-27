---
layout: post
title: Jekyll Robots Configuration
description: This post shows how to enable robots meta tag in Jekyll-built blogs. It's super easy without plugins.
tags: jekyll blog robots
---


<style>
.highlight-left {margin-left: 0}
</style>

Sometimes we want to tell search engines to index our pages, but sometimes we don't. [Search Engine Optimization](https://moz.com/beginners-guide-to-seo) helps you make your pages appear at better location, while [robots meta tag](http://www.robotstxt.org/meta.html) can prevent search engine to crawl certain pages. For my blog, I don't want search engine to index the tag pages.

Ultimately, I want the following html meta tag appear in all the tag pages.

{% highlight html %}{% raw %}
<meta name="robots" content="noindex" />
{% endraw %}{% endhighlight %}{: .highlight-left }

To achieve this result, we need to modify the front matter of tag pages, and add a few lines to the format of head section of pages.

### Front Matter

For all tag pages, let's add a new property `robots` to its front matter:

```
---
layout: tagpage
title: "Tag: hololens"
tag: hololens
robots: noindex
---
```

Then, for all tag pages, it has an additional property accessed via `page.robots`.

If you are curious about how to create tag pages, please visit this [post](http://longqian.me/2017/02/09/github-jekyll-tag/).

### Head Element

In the layout of the head section, usually at `_includes/head.html`, the following lines should be added to correctly add `robots` meta tag.

{% highlight html %}{% raw %}
{% if page.robots %}
  <meta name="robots" content="{{page.robots}}" />
{% endif %}
{% endraw %}{% endhighlight %}{: .highlight-left }

Then, **jekyll serve!**

Thanks for reading!  <i class="em em-lq"></i>

