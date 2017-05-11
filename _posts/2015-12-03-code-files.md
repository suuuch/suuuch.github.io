---
title: 代码存档：Python读取路径下所有文件，文件夹
layout: post
author: Suuuch
category: Python
tags:
- python
---


python读取路径下所有的文件以及文件夹：

函数声明：`os.walk(top,topdown=True,onerror=None)`

(1)参数`top`表示需要遍历的顶级目录的路径。

(2)参数`topdown` 的默认值是`“True”`表示首先返回顶级目录下的文件，然后再遍历子目录中的文件。当`topdown`的值为"False"时，表示先遍历子目录中的文件，然后再返回顶级目录下的文件。

(3)参数`onerror`默认值为"None"，表示忽略文件遍历时的错误。如果不为空，则提供一个自定义函数提示错误信息后继续遍历或抛出异常中止遍历。

返回值：函数返回一个元组，含有三个元素。这三个元素分别是：每次遍历的路径名、路径下子目录列表、目录下文件列表。

{% highlight python %}
def get_files(rootDir):
    list_dirs = os.walk(rootDir)
    for root, dirs, files in list_dirs:
        for d in dirs:
            pass
            #print os.path.join(root, d)
        for f in files:
            path = os.path.join(root, f)
            if path.endswith('view.py'):
                #print path
                info = get_key_form_code(path)

{% endhighlight %}
