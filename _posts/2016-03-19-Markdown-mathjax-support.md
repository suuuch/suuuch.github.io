---
title: 在Markdown添加MathJax以支持数学公式
layout: post
author: Suuuch
category: MathJax
tags:
- MarkDown
- MathJax
---

使用Jekyll写作文章的时候有可能需要内嵌一些数学公式, MathJax就是用来干这个的，试用了一下感觉非常方便。步骤如下:
修改html头部。

在每个页面开头加上这么一句，在Jekyll下可以通过修改default.html加上。

```
<script type="text/javascript" async 
    src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.1/MathJax.js?config=TeX-AMS-MML_HTMLorMML"> 
</script>

```

修改_config.yml，把markdown选项修改为:
markdown: kramdown
然后在发布的时候就可以使用$$来把需要显示的数学式子扩起来。像这样：

```
$$a^2 + b^2 = c^2$$
```

例子：

$$a^2 + b^2 = c^2$$

发布出来就是漂亮的公式了。

一些更酷的例子：
不过我可能永远用不到这么复杂的表达式 :).
