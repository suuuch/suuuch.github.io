---
layout: post
title: "Kramdown学习笔记"
data: 2016-04-13
categories: note
tags:
- bumbling
- jekyll
- Markdown
- kramdown
---

## 新博客框架 {#fir_id}

这是我的第一篇使用Jekyll写的博文\\
This is the first post using Jekyll.

博客使用的框架是[jekyll](https://jekyllrb.com/)，模板来自[Travelogue](https://github.com/SalGnt)\\
This blog is based on [jekyll](https://jekyllrb.com/), and template comes from [Travelogue](https://github.com/SalGnt)

这里的博文是用Markdown标记语言书写的。\\
The post was written with Markdown language.

## Markdown和kramdown

Markdown是一种标记语言。可以通过简单的一些符号来展示网页、PDF或者WORD中的表格、链接、图片、分级标题、文本加粗等等效果。例如以下的markdown文本(下左)会被转化成不同标题(下右)的形式

~~~~
# MD一级标题
## MD二级标题
### MD三级标题
~~~~
{::comment}
{:hstack2="left"}
{:/comment}

> # MD一级标题
>
> ## MD二级标题 #####
>
> ### MD三级标题 ########

{::comment}
{:hstack2="end"}
{:/comment}

比如本段和后文的标题都是二级标题，它们都是按照这种`## 标题`方式标记的。

Markdown的好处在于就算用一个记事本也能写出包含图片、链接、不同字体的文章。我们常见的写作环境有Word, OneNote，Wordpress这一类编辑器，通过菜单操作来修改文章的样式；也有Latex这种纯命令形式的编辑环境，文章样式必须通过LaTeX命令设置，之后再进行编译和渲染得到PDF。对于前者，整个写作过程是所见即所得的，也就是说设置一个文本加粗或者插入一个图片，可以直接看到结果；但是缺点是样式的调整有时候会很蛋疼。特别是涉及到比较复杂的排版的时候。多次使用Word进行论文排版之后，我仍旧认为Word的排版有时候是一门玄学：随便动一个地方可能导致整个文章的样式都乱套，就算没有乱动，也不能保证文章样式正确。但是对于LaTeX，众多的包（package）和丰富的命令能够让一个熟练用户兼顾排版的自定义程度和排版的效率。对于有一定基本功的用户，并不会那么容易出现全文样式错乱的问题。但是LaTeX的缺点也很明显，就是陡峭的学习曲线。对于非计算机类的学生，学习LaTeX的初期会很痛苦。但是花一两天看完LaTeX的入门教材，对LaTeX的设计理念有了初步了解之后，对于从古自今的文章排版会从认识会上一个新的台阶。

那么相比前面两种编辑软件，我以为Markdown的优势主要在于方便。首先，使用Markdown的环境主要是网页环境。也就是说Markdown代码最后会转化成html。因此Word、OneNote的文字处理能力并没有用武之地；Wordpress这类在线编辑器可以把文字处理结果直接转化成html，但是通常需要打开这样的编辑器才能写作；如果徒手写HTML的话，虽然可以呈现出更加丰富的视觉效果，但HTML代码和正文混在一起非常碍眼。而Markdown的博文可以直接在Sublime、atom这类文本编辑器中编辑，对于写作环境的要求很小。其次，对于网页环境，Markdown的标记（类似LaTeX中的命令或者HTML的TAG）非常精简。常见的换行、标题、插入链接和图片都可以利用简单的符号表示。所以，Markdown很适合于博客的写作环境。

当然，Markdown同样是有缺点的。它并不是所见即所得的。如果中间有错误的话，需要找到产生错误的位置，重新修改再转换成HTML。其次，转换这个过程和转换引擎有关。Markdown只是一种标记语言，那么转化的结果自然就依赖于转换引擎的标准、语法和实现细节。[目前](https://en.wikipedia.org/wiki/Markdown#Standardization)，Markdown还没有形成统一的、完整的语言规范。因此不同的Markdown转换引擎就会在基本的Markdown语法中加入自己的拓展和修改。比如Jekyll默认是使用的[kramdown](http://kramdown.gettalong.org)引擎来把Markdown转换成HTML。虽然目前常见的Markdown都是转换成HTML，但是这并不是Markdown的唯一目的。Markdown的设计理念就是提供一种方便的、标记某类文体（比如用户手册、在线文档这类文体）的方式。而最终呈现的形式，可以是网页，也可以是PDF、电子书等等。

kramdown是一套比较高效的markdown转换引擎。它所支持的Markdown语法可以去[这里](http://kramdown.gettalong.org/syntax.html)查看。相比于标准(常用但没有形成规范)的Markdown，kramdown进行了更多的拓展。同时对Markdown语言的一些细节地方进行了具体化。这里针对几个常见的标记进行介绍。

### Markdown基本元素

Markdown文档主要由两大类元素构成。一类是block，一类是Span。可以理解为block单独成一“段”。比如本节标题，前后都是空行。这就是一个block。再比如现在你看到的这个自然段的文本就是一个block。

类似地，这一段转成了另外一个block级的元素。除此之外，列表、大块代码区域都是block级的元素。block和block元素是不能“并列”排在一起。

而Span元素则通常是指小的文本，可以在文本中间出现。比如`行内代码`，*行内的强调*或者一个[行内链接]('#')都是Span元素。Span可以在Block元素内部，或者Span元素内部。

### 分级标题

前文提到Markdown语法可以通过加`#`来定义标题级别，kramdown更进一步，可以在定义标题级别的时候定义标题的ID。这样做的效果是，转化后对应的h1,h2,h3...的id属性会变成设置的值。例如：

~~~~
# Markdown一级标题  {#fir_id}
## Markdown二级标题 {#sec_id}
### Markdown三级标题 {#thr_id}
~~~~


### 列表元素


#### 基本列表

Markdown可以通过*和数字来分别定义无序和有序列表。例如：

~~~~
* kram
+ down

1. kram
2. down
3. now
~~~~

会得到：

* kram
+ down

1. kram
2. down
3. now

#### 嵌套列表

在此基础上，也可以定义嵌套列表：

~~~~~
*   First item

    A second paragraph 另起一段

    * nested list 嵌套列表

    > blockquote 引用块

*   Second item
~~~~~

这样将会得到：

*   First item

    A second paragraph 另起一段

    * nested list 嵌套列表

    > blockquote 引用块

*   Second item

在用Markdown写列表的时候，需要注意的是保持缩进。也就是列表项之间，同一个列表项中的所有元素之间，需要保持同样的缩进。否则可能出现意料之外的情况。虽然kramdown支持把tab转换成4个空格，但是jekyll让用户尽量不要使用tab，否则可能产生错误。因此写Markdown的列表的时候，最好通过空格缩进。也可以在sublime、notepad++这类编辑器中，把tab设置成对应四个空格的形式。

#### 定义列表

定义列表是kramdown对标准Markdown的拓展。定义列表用于在文章中对一个或者多个术语进行定义。它的基本形式是：在属于之后另起一行，以英文冒号，空格之后跟具体定义文本。一个术语可以有多个定义。定义列表也可以嵌套。举例如下：

~~~~~~~
术语
: 定义1

: 定义2
~~~~~~~
{:hstack3="left"}


> 术语
> : 定义1
>
> : 定义2
> ^
> &nbsp; 
{:hstack3="left"}

~~~~~
<dl>
  <dt>术语</dt>
  <dd>定义1</dd>
  <dd>
    <p>定义2</p>
  </dd>
</dl>
~~~~~
{:hstack3="end"}

上面的左框是Markdown的原文，中间是转化之后显示的效果。初看中间的结果可能决定定义列表并没有什么用。因为目前这种外观完全可以用常规文本分行实现。事实上，kramdown会把这种列表处理成新的html元素，也就是最右边的代码区域中内容。可以发现，对于定义列表，kramdown生成了新的HTML元素dl。这样一来，我们可以在自定义的CSS中来定义dl、dt以及dd元素的样式，从而让定义列表的显示效果完全不同。

### 代码区域

kramdown可以指定一段Markdown文本不进行转换。这个区域的文本就是代码区域（code block）。要注意的是代码区域并不是标准的的Markdown语法的一部分，所以在别的环境中这部分的Markdown可能不会正确解析。kramdown允许几种方法来指定代码区域：

*	前置空格：\\
	文本前有四个空格的时候，这行文本会作为代码区域，不会进行编译。比如：

~~~~
    * 前有4个空格。下一行#前也有空格。**这个强调不会被编译**

    ## 这一行文本不会被编译成二级标题.
~~~~

*	波浪符号：\\
	一段文本被前后两行波浪符号包围的话，这段文本作为代码区域，不会被编译。如果代码区域中也想有波浪符号，只需要保证内层的波浪符号不必外层的波浪符号长即可。比如：

~~~~~~~~~~~~
~~~~~~~
~~~~
波浪符号中的内容不会被转换
~~~~
~~~~~~~~
~~~~~~~~~~~~~~~~~~

### 代码高亮

在此基础上，如果我们希望有代码高亮，可以根据[这里](http://jekyllrb.com/docs/installation/#optional-extras)使用Pygments或者Rouge。kramdown支持对代码区域传递[IAL](http://kramdown.gettalong.org/syntax.html#inline-attribute-lists)来指定这个区域使用的语言。比如使用：

~~~~~~~~~~~~~~
~~~
def what?
  42
end
~~~
{: .language-ruby}
~~~~~~~~~~~~~~

这一段在生成html之后，其中\<code\>节点会增加一个属性来描述这一段内容是什么语言：`class="language-ruby"`。这样就可以利用Rouge或者Pygments对这个区域进行高亮。

因为Jekyll除了使用kramdown之外还有别的组件，比如Liquid。因此可以使用如下方法快捷地进行代码高亮。

~~~~~~~~~~
{% raw %}
{% highlight scss %}
.container {
    background: $background-color;
    padding: 0;

    @include media-query($on-palm) {
        background: rgba($background-color, .95);
        width: 100%;
    }
}
{% endhighlight %}
{% endraw %}
~~~~~~~~~~

其效果是：

{% highlight scss %}
.container {
    background: $background-color;
    padding: 0;

    @include media-query($on-palm) {
        background: rgba($background-color, .95);
        width: 100%;
    }
}
{% endhighlight %}

### 图像和链接

标准的Markdown语言就已经对插图图片和链接有很好的支持了。kramdown同样也进行了一些扩展。对于Markdown来说，插入图片的方式是：`![标题](图片链接)`,而链接的插入方式是`[标题](url)`。

![](/assets/images/post_images/cat1.jpg)

除此之外，图片和链接都支持定义模式。也就是可以定义一个图片或者链接，然后引用。比如：

~~~~
引用部分
And here is a referenced ![smile] [smile2]
This is a [reference style link][linkid] to a page.

定义部分

[smile]: smile.png

[smile2]: smile2.png
{: height="36px" width="36px"}

[linkid]: http://example.com
~~~~

引用模式包括引用部分和定义部分。定义一个图片或者链接的方法是。给需要定义的图片或者链接设一个名字，用方括号包围。方括号之后加一个冒号和空格。后跟图片或者链接的URL。

在引用的时候只需要用方括号包围对应的名字。如果是图片引用，那么在方括号之前还需要加一个叹号`!`。

smile2的图片定义之后还有一个花括号`{}`包围的内容。那是[后文](#ial)介绍的IAL，在这里它的作用是定义图片的大小。

对于链接，还有一种最快捷的标记方式，那就是在尖括号`<>`中间直接加入URL。比如`<http://caunion.me>`得到<http://caunion.me>。这种方法插入的链接无法改变链接现实的名称。

### 数学公式

如果我们想在文章中呈现数学公式，kramdown也提供了一些帮助。kramdown拓展了Markdown语法，采用了类似$$\LaTeX$$的方式来标记数学公式区块。在区块的内部，用户可以写$$\LaTeX$$命令。代码区块一样，数学公式可以解析成Block级元素（单独区块）和Span级元素（行内形式）。比如`$$E = mc^2$$`，得到的就会是$$~E = mc^2$$这种行内公式。再比如：

{% highlight latex %}
$$
\begin{align*}
  & \phi(x,y) = \phi \left(\sum_{i=1}^n x_ie_i, \sum_{j=1}^n y_je_j \right)
  = \sum_{i=1}^n \sum_{j=1}^n x_i y_j \phi(e_i, e_j) = \\
  & (x_1, \ldots, x_n) \left( \begin{array}{ccc}
      \phi(e_1, e_1) & \cdots & \phi(e_1, e_n) \\
      \vdots & \ddots & \vdots \\
      \phi(e_n, e_1) & \cdots & \phi(e_n, e_n)
    \end{array} \right)
  \left( \begin{array}{c}
      y_1 \\
      \vdots \\
      y_n
    \end{array} \right)
\end{align*}
$$
{% endhighlight %}

可以得到Block级单独公式区块。

$$
\begin{align*}
  & \phi(x,y) = \phi \left(\sum_{i=1}^n x_ie_i, \sum_{j=1}^n y_je_j \right)
  = \sum_{i=1}^n \sum_{j=1}^n x_i y_j \phi(e_i, e_j) = \\
  & (x_1, \ldots, x_n) \left( \begin{array}{ccc}
      \phi(e_1, e_1) & \cdots & \phi(e_1, e_n) \\
      \vdots & \ddots & \vdots \\
      \phi(e_n, e_1) & \cdots & \phi(e_n, e_n)
    \end{array} \right)
  \left( \begin{array}{c}
      y_1 \\
      \vdots \\
      y_n
    \end{array} \right)
\end{align*}
$$

如果你直接按照上面的代码尝试的话，可能什么都得不到。这是因为，同样和代码区块一样，kramdown不参与具体的公式渲染，只是把数学公式区域生成单独的HTML元素（SCRIPT元素）。需要我们自己使用别的工具渲染对应SCRIPT元素。

目前渲染$$\LaTeX$$公式的JS库主要有MathJax和KeTaX。它们的使用都需要在jekyll的layout中加入对库的引用。Jekyll默认尝试调用MathJax进行渲染。如果MathJax不存在，那么就不渲染。如果使用KaTeX的话，则需要自己在页面的JS中加入渲染的命令。

现在也有不少人使用KaTeX来渲染$$\LaTeX$$的数学公式，因为KaTeX被认为有更快的渲染速度。但是我测试过后发现，KaTeX对$$\LaTeX$$的语法支持并不完善。比如换行命令`\\`,`\newline`就不被支持，同时让多个公式居中对齐的`\beigin{align} \end{align}`也无法使用。这样一来，如果有多行公式，就需要对每一个公式单独一行用来写。但是从KaTeX的issue页面来看，作者已经快完成对`\begin{align}`这类命令的支持了。如果好用，我之后可能也会重新换回KaTeX。

### 尾注标记

尾注标记并非标准Markdown的语法，而是kramdown的拓展[^footnote-doc]。

尾注主要由尾注标记和尾注定义组成。尾注标记的使用就是在方括号中设置对应的尾注名称，同时尾注名称以`^`符号开头。尾注名称通常是数字或者一个词语。比如：

~~~
这是正文部分。这是一段文本[^1]。这是另外一段文本[^footnote]。
~~~

尾注标记会把同样名字的尾注连接到同一个尾注定义上去。也就是说，尾注的命名并不要求按照数字顺序。因为顺序会按照尾注在文章中出现顺序重新排列。尾注标记和尾注定义的名字必须比配才能正确连接上。否则，这个尾注将不会转化成功。

尾注定义主要是用来定义尾注的具体内容。它的形式和图片、链接引用定义类似。也是以一个方括号开始，方括号中是对应的尾注名字。方括号之后是冒号。冒号之后可以跟若干空格。然后就是尾注的正文。注意，尾注是Block级的元素。所以可以包含Block或者Span元素（类比List）。举例如下：

~~~~
[^1]: Some *crazy* footnote definition.

[^footnote]:
    > Blockquotes can be in a footnote.

        as well as code blocks

    or, naturally, simple paragraphs.

[^other-note]:       no code block here (spaces are stripped away)

[^codeblock-note]:
        this is now a code block (8 spaces indentation)
~~~~

[^footnote-doc]: 引用自http://kramdown.gettalong.org/syntax.html#footnotes

尾注定义的内容放在什么地方并不重要。最后生成的尾注都会被kramdown自动放到文章的最后。如果多个尾注定义的名字重复，那么只保留最后出现的那个[^footnote-doc]。

### IAL属性列表

[IAL](http://kramdown.gettalong.org/syntax.html#inline-attribute-lists)(Inline Attribute Lists)也是kramdown对基本Markdown语法的拓展。其目的是给Markdown的标记添加属性。如果Markdown是转化成HTML，添加的属性就是最后生成的HTML元素的属性。通过这种方法，可以对Markdown的文本实现细粒度的样式定义和脚本控制。

就像Markdown文本主要由Block和Span元素构成，IAL也可以分别针对Block级元素和Span级元素添加属性。二者的语法基本一致。比如：

~~~~~~
给一段文本（Block级元素）添加属性id='param-one'
{: #para-one}  

> 给一段引用区域（block级）添加title='TBT'和id='myid'
{:title="TBT"}
{: #myid}

{:.ruby}
    前置4空格的代码区域（Block），添加class='ruby'

给行内*强调*{:.underline} 这个Span级元素添加class='underline'属性；

给行内[链接](test.html){:rel='haha'}这个Span级元素添加rel='haha'属性；
~~~~~~

IAL的基本语法是`{:attribute="value"}`，需要添加多个属性可以并列。事实上，我们在前面提到的“标题元素”，kramdown提供的`{#fir_id}`本质上就是给每个标题添加一个IAL。

在Markdown文本转换成HTML之后，我们就可以利用CSS或者JS对某些标记了特殊属性的元素单独控制。比如在“定义列表”那一节，我把三个代码块并排安排在同一行了，实现了Markdown多列元素的控制。这背后的方法就是利用IAL的方法，给那三个区域添加了hstack属性，同时在CSS中对这个属性的元素设置了单独的样式。

### 拓展语法

这部分的内容仍然是kramdown对标准Markdown语法的拓展。恰当使用可以增加Markdown的表达能力。拓展语法部分类似于编译参数。主要有三种：comment、nomarkdown和options。使用语法和IAL类似。

~~~~~
注释部分{::comment}Markdown注释{:/comment}?
{::comment}这一部分是注释 comment{:/}不会转换和输出

{::options key="val" /}
~~~~~

1.	comment: 包围的部分作为Markdown注释。不会转化，不会输出
2.	nomarkdown: 被包围的部分不被kramdown转换，而是根据这部分的type属性指定的转化器转化输出。如果没有指定转化器，那么就让每个可用的转换器处理之后输出。
3.	这个命令不能包围内容，而是单独存在。用于设置kramdown的全局选项（比如进制自动给Header产生ID属性）。

### 尾注示例