​		Gitbook是一个命令行工具，可以把你的Markdown文件汇集成电子书，并提供PDF等多种格式输出。你可以把Gitbook生成的HTML发布出来，就形成了一个简单的静态网站。Gitbook还有一个同名的平台（gitbook.io），可以发布和销售电子书，并提供了一个Markdown客户端工具（支持Mac、Windows和Linux）帮助写作。以下是我在使用Gitbook中的笔记。

**第1步**

安装npm（Node Package Manager）。从node.js的[官网](http://nodejs.org/#download)上下载安装程序，即可完成Node.js和npm的安装。

**第2步**

通过npm安装Gitbook。

```git
$ npm install gitbook -g
```

完成后花10分钟阅读下Gitbook的[帮助文档](http://help.gitbook.io/)。如果你没耐心看手册，那就继续往下读吧

**第3步** 
了解Gitbook的基本规则。

Gitbook需要2个基本文件：

README.md
SUMMARY.md
README.md是关于你的书的介绍，而SUMMARY.md中则包含了书目，即章节结构，它的格式大致是：

* [第1章](c1.md)

 * [第1节](c1s1.md)

 * [第2节](c1s2.md)

* [第2章](c2.md)

剩下的东西就很好理解了，你只需要编写相应章节即可。在编辑完README.md和SUMMARY.md后，你可以运行以下命令：

```
$ gitbook serve -p 8080 
```

Gitbook首先把你的Markdown文件编译为HTML文件，并根据SUMMARY.md生成书的目录。所有生存的文件都保存在当前目录下的一个名为_book的子目录中。完成这些工作后，Gitbook会作为一个HTTP Server运行，并在8080端口监听HTTP请求。

运行以上命令后，打开浏览器，在地址栏输入：http://localhost:8080即可看到你的书页了。

其中位于左侧书目顶部的Introduction一节就编译自README.md，而书目本身自编译自SUMMARY.md。你要在自己的网站上发布新书，只需把_book目录复制到服务器相应目录即可。至此Gitbook的基本用法就介绍完毕。下面简单讨论下Gitbook的其他应用，包括Gitbook的插件、与Github的融合、Gitbook客户端、Gitbook平台，以及Gitbook的问题。

Gitbook的插件支持

Gitbook可以生成HTML，因此它支持一些外部的JavaScript文件嵌入到HTML中，例如Google统计、Disqus评论系统等。以下以页面中嵌入Disqus评论为例。

首先是安装Gitbook的Disqus插件。

```
$ npm install gitbook-plugin-disqus
```

然后建立一个book.json文件，其格式如下：

```
{
  "plugins": ["disqus"],
  "pluginsConfig": {
    "disqus": {
      "shortName": "NAME-FROM-DISQUS"
    }
  }
}
```


把上面的NAME-FROM-DISQUS修改为你在Disqus上的项目名即可。

再次运行命令：

```
$ gitbook serve -p 8080 .
```

并刷新浏览器，即可看到附加了Disqus评论的页面。

与Github的融合
Gitbook的博客上说Github提供了对Gitbook的特殊支持，但我没有测试。只是依然把源文件保存在Github上，然后用Gitbook去编译。期待Gitbook做的更好。

Gitbook客户端
Gitbook客户端支持Mac、Windows、Linux。我在Mac和Windows简单尝试了这个客户端，总体而言可以用。但也仅仅是可以用而已。你可以在客户端里编辑Markdown文件，并提供一个实时的预览窗口；可以关联到你的Gitbook账户，并把内容同步到gitbook.io，并为你生成PDF等。说句题外话，如果你要Markdown的客户端的话，飞象马克更好用，至少Vim编辑模式你得支持啊。

生成图书
当你在自己的电脑上编辑好图书之后，你可以使用Gitbook
的命令行进行本地预览：

```
$ gitbook serve .
```

然后浏览器中输入 http://localhost:4000 就可以预览生
成的以网页形式组织的书籍。
这里你会发现，你在你的图书项目的目录中多了一个名为
_book的文件目录，而这个目录中的文件，即是生成的静态
网站内容。
使用build参数生成到指定目录
与直接预览生成的静态网站文件不一样的是，使用这个命令，
你可以将内容输入到你所想要的目录中去：

```
$ mkdir /tmp/gitbook
$ gitbook build --output=/tmp/gitbook
```

输出PDF文件
输入为PDF文件，需要先使用NPM安装上gitbook pdf：

```
$ sudo npm install gitbook-pdf -g
```


