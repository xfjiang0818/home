# Links and Navigation

链接分为两种

* 内部链接：链接到自己网站中的另一个页面
* 外部链接：链接到另一个站点



## 1. Basic Links

使用\<a>元素指定链接



### 1.1 Linking to Other Web Pages

链接到另一个web页面，\<a>必须有herf属性，属性的值是链接到的文件的名称

```html
<body>
    <p>Return to the <a herf="index.html">home page</a>.</p>
</body>
```

链接到另一个站点时，需要指定完整的web地址

```html
<body>
    <p>Why not visit the <a herf="http://www.wrox.com/">Wrox web site</a>.</p>
</body>
```

可以使用title，使得鼠标悬停时显示访问内容的描述

```html
<p>
    <a herf="http://www.Google.com/" title="Search the Web with Google">Google</a> is a very popular search engine.
</p>
```

需要注意的是，\<a>中所有的元素都将表现为来链接，因此需要避免在\<a>之后和\</a>之前加空格



### 1.2 Linking to E-mail Address

显示邮件的链接，在点击时打开自己的邮件程序并创建新邮件

```html
<a herf="mailto:name@example.com">name@example.com</a>
```

这样做的坏处：一些人会使用程序搜索网上的邮件地址并发送垃圾邮件

* 使用访问者填写的e-mail表单，这需要使用ASP.NET或PHP脚本
* 使用Javascript写e-mail地址



## 2. Understanding Directories and Directory Structures

目录（*directory*）是网站上的文件夹的别名，网站包含目录就像硬盘包含文件夹一样

重要术语

* 根目录（*root directory*）
* 子目录（*subdirectory*）
* 父目录（*parent directory*）



## 3. Understanding URL

![image-20200215223559933](C:\Users\姜晓飞\AppData\Roaming\Typora\typora-user-images\image-20200215223559933.png)

**Scheme**：标识文件的传输方式，大多数网站使用超文本传输协议（HTTP）。

> https 是 http 的更安全的形式，常用于网上银行
>
> ftp 常用于下载大文件

**Host address**：有时是IP地址（一些数字），通常是站点的域名，这里是wrox.com，www不是域名本身的一部分。

> 所有连接到Internet的计算机都可以使用IP地址找到，IP地址是一组最多12位的数字，由句号分隔。在浏览器输入一个域名的时候，域名将在后台转换为储存web site的IP地址。
>
> 这是通过查询域名服务器（DNS，domain name server）实现的，DNS保存域名目录和相应的IP地址。

**Filepath**：通常由正斜杠（forward slash character）开头，包含一个或多个目录名，文件路径可能以文件名结尾。

> 不仅网页有URL，网上的每个文件，包括每个图像，都有自己的URL。

如果没有给出文件名，web服务器会根据配置执行以下三种操作之一：

* 寻找并返回一个默认文件。使用XHTML编写的网站，默认文件通常是index.html；在没有指定filepath时，服务器会在根目录中寻找index.html，如果指定了一个目录，服务器会在该目录中寻找index.html。
* 提供该目录下的文件列表
* 显示一条消息，表明无法找到页面或者无法浏览文件夹中的文件

链接到自己的网站上的页面时，不需要使用全部三个部分，只需要使用filepath和filename。



### 3.1 Absolute and Relative URLs

Absolute URL包含在Internet上唯一标识特定文件所需的所有内容

Relative URL表示资源相对于当前页面的位置

> 浏览器会将 Relative URL 转换成 Absolute URL
>
> Relative URL 的优势是在域名变化时不必进行大量的改动

**注意**：Relative URL 仅对同一网站内的连接起作用，不能使用它们链接到其它域名 *domain name* 上的页面

#### Same Directory

在同一目录下的页面直接写文件

```html
contactUs.html
```

#### Subdirectory

子目录

```html
film/index.html
```

#### Parent Directory

```html
../index.html
```

#### From the Root

相对于根目录的路径

```html
/contactUs.html
/Entertainment/Music/index.html
```



### 3.2 The \<base> Element

当浏览器遇到一个 Relative URL 时会将它转变为一个完整的 Absolute URL。\<base> 元素为一个页面指定一个基本 URL，当浏览器遇到 Relative URL 时都会添加到这个页面。

```html
<base href="http://www.exampleSites2.com" />
```

Relative URL

```html
Entertainment/Arts/index.html
```

Absolute URL

```html
http://www.exampleSites2.com/Entertainment/Arts/index.html
```

\<base> 只能携带 href 属性和 id 属性



## 4. Creating Links with the \<a> Element

一个页面上所有可见的链接都是 *source anchor*

可以使用 \<a> 元素在页面的某些部分创建标记，这些标记允许直接链接到页面的该部分，这些标记称为 *destination anchors*

### 4.1 使用 href 属性创建 source anchor

没啥

### 4.2 使用 name 和 id 属性创建 destination anchor

链接到页面的特定部分，常见示例如下

* Back to top
* content
* 脚注、定义

使用 \<a> 元素，但是用的时 id 属性而不是 href 属性。name 在旧的网页中使用，id 在 html4 中引入。

```html
<p>This page covers the following topics:
    <ul>
        <li><a href="URL">URLs</a></li>li>
        <li><a href="SourceAnchors">Source Anthors</a></li>
        <li><a href="DestinationAnchors">Deatination Anthors</a></li>
        <li><a href="Examples">Examples</a></li>
	</ul>
</p>

<h1>Linking and Navigation</h1>
<h2><a id="URL">URLs</a></h2>
<h2><a id="SourceAnchors">Source Anchors</a></h2>
<h2><a id="DestinationAnchors">Destination Anchors</a></h2>
<h2><a id="Examples">Examples</a></h2>
```

指示顶部

```html
<h1><a id="top">Linking and Navigation</a></h1>
```

如果想从其它的网站直接链接到该网页的特定部分，输入

```
http://www.example.com/HTML/links.html#SourceAnchors 
```

**注意：是 href 而不是 herf ！**



### 4.3 \<a> 还有一堆乱七八糟的属性



## 5. Advanced E-mail Links

打开默认的电子邮件编辑器

```html
<a href="mailto:info@example.org">info@example.org</a>
```

还可以指定邮件的其他部分，比如主题、正文、地址，用的时候回来查表就好

```html
<a href="mailto:info@example.org?subject=Inquiry&cc=sales@example.org">info@example.org</a>
```







