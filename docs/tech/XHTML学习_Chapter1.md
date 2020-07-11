# HTML

### 1. 什么是 HTML

**HTML**是超文本标记语言（Hypertext Markup Language）

> HTML 的开发是由 W3C（World Wide Web Consortium）负责监督的
>
> HTML4.01 是 1999 年 10 月诞生的，2000 年 1 月添加了一些更严格的规则成为 XHTML

**XHTML**是可扩展超文本标记语言（Extensible Hypertext Markup Language）

HTML 是一种**标记语言**（makeup language）

HTML 使用**标记标签**（makeup tags）描述网页

-----

### 2. HTML 标签

```html
<html>
    <head>
        <title> 我的标题 </title>
    </head>
    <body>
        <h1> 我的第一个标题 </h1>
        <p> 我的第一段 </p>
        <p> 我的第二段 </p>
    </body>
</html>            
```

HTML 标签是成对出现的，分为*opening tags*和*closing tags*

一对标签与之间的内容称为一个*element*

如果一个*element*包含另一个*element*那么前者称为*parent*，后者称为*child*

有些 Web pages 的 HTML tags 使用了大写字母，**XHTML 要求始终使用小写字母**

**<html>** 整个 web page 在 <html> 与 </html> 之间，<html> element 分为两部分

**<head>** 包含页面的信息，不是页面的主要内容

**\<body>** 真正通过浏览器窗口看到的内容

**\<title>** 浏览器在上方显示的页面标题，也是收藏到书签时的标题

**\<a>** 链接，\<a> 和\</a> 之间是点击的文本

```html
<p>
    <a href="http://www.Google.com" target="_blank">
        Click here to visit Google's Web site.
    </a>
</p>
```

href 和 target 称为属性（attribute），由*name*和*value*组成

**所有 XHTML 属性名要求使用小写字母**

-----

### 3. 基本文本格式

##### 多个空格与换行

element 中两个 tags 之间的内容自带*white space cllapsing*功能，即无论手动输入多少个空格或者换行，在浏览器页面中都仅显示一个空格，利用这一点可以使代码更方便阅读。

浏览器会自动换行。

##### 使用\<hn> 产生标题

XHTML 提供了 6 个级别的标题\<h1>\<h2>\<h3>\<h4>\<h5>\<h6>

大多数浏览器的\<h1>\<h2>\<h3> 比默认文本字号大，\<h4> 的相同，\<h5>\<h6> 的小

\<hn> 可以携带*universal*属性和*align*属性

##### *align*属性（不建议使用）

指定 heading 的位置（左中右）

可以被 CSS 替代

##### 使用\<p> 产生段落

\<p> 可以携带*universal*属性和*align*属性

##### 使用\<br /> 换行

\<br /> 是一个*empty element*，不需要*opening tags*和*closing tags*

早期版本的 HTML 中有\<br> 的写法，但是**XHTML 中必须写成\<br />**

可以使用多个\<br /> 空出多行，有些人使用\<br />\<br /> 来分段而不是\<p>，二者的效果差不多

```html
Paragraph one<br /><br />
Paragraph two<br /><br />
```

但是 XHTML 是描述结构的语言，这种做法并不是在描述结构

严格来说\<br /> 应该使用在*block-level element*中，例如\<p> element

\<br /> 可以携带的属性有 clear，class，id，style，title

##### 使用\<pre> 创建预格式化文本

\<pre> 和\</pre> 之间的内容完全遵照源代码的格式，多空格不会自动折叠，不会根据浏览器窗口自动换行，仅在设置换行符的位置换行，最常见的用途是显示代码。

\<pre> 和\</pre> 之间的字符是等宽字体（monospaced font），例如 Courier，所有字符的宽度是一样的，而非等宽字体（non-monospaced font）中，*i*和*m*的宽度就会明显不同。

制表符（tab character）可以在\<pre> 中起作用，一个制表符占 8 个空格，但是不同的浏览器中制表符的实现是不同的，因此应该尽量使用空格。

> Firefox IE Safari 支持\<nobr>，作用是防止自动换行并且不会使用 monospaced font，但\<nobr> 属于扩展，不是 XHTML 规范的一部分。

-----

### 4. 表象元素（presentational elements）

|     Element      |         Function         |            |
| :--------------: | :----------------------: | :--------: |
|       \<b>       |         **加粗**         |            |
|       \<i>       |          *斜体*          |            |
|       \<u>       |          下划线          | 不建议使用 |
| \<s> 或\<strike> |          删除线          | 不建议使用 |
|      \<tt>       |         等宽字体         |            |
|      \<sup>      |           上标           |            |
|      \<sub>      |           下标           |            |
|      \<big>      | 比周围大一个字号，可嵌套 | 不建议使用 |
|     \<small>     | 比周围小一个字号，可嵌套 | 不建议使用 |
|     \<hr />      |      创建一条水平线      |            |

-----

### 5. 短语元素（phrase elements）

与表象元素类似，有相似的效果，但不仅仅描述显示效果，还要表达内容，比如\<i> 和\<em> 显示效果很像，但后者还表示强调。朗读程序可以据此添加重音，搜索程序可以查找关键词，因此不能因为显示效果相像就只使用表象元素。

以下所有短语元素都可以携带*universal*属性和*UI event*属性。

**注意：文本的显示效果不是 XHTML 的重点，CSS 可以轻易地完成这件事，短语元素的使用意义是内容的表达**

|    Element    | Function               |                                                              |
| :-----------: | :--------------------- | :----------------------------------------------------------- |
|     \<em>     | 强调，通常是斜体       |                                                              |
|   \<strong>   | 强烈强调，通常是粗体   |                                                              |
|  \<address>   | 地址，通常斜体         |                                                              |
|    \<abbr>    | 缩写词，下划线         | title 属性描述缩写前的文本；xml:lang 指示使用的语言          |
|  \<acronym>   | 首字母缩略词，下划线   | title 属性描述缩写前的文本；xml:lang 指示使用的语言          |
|    \<dfn>     | 特殊术语               | 第一次引入时使用                                             |
| \<blockquote> | 引用文本，左右缩进     | cite 属性指示引用的来源，应指向在线文档的 URL 以及其确切位置 |
|     \<q>      | 简短的引用，添加双引号 | cite 属性指示引用的来源                                      |
|    \<cite>    | 引用源，通常斜体       | 在线文档将\<cite> 放在\<a> 中                                |
|    \<code>    | 代码，等宽字体         | 通常和\<pre> 一起使用保持代码格式；使用 <和> 时应使用转义字符\&lt;和\&gt; |
|    \<kbd>     | 键盘输入指示           |                                                              |
|    \<var>     | 编程变量               | 通常与\<pre>\<code> 一起使用，指示该元素的内容是一个可以提供的变量 |
|    \<samp>    | 程序输出               |                                                              |

-----

### 6. Lists

列表分为无序列表、有序列表和定义列表

##### \<ul> 元素创建无序列表

```html
<ul>
    <li>Bullet point number one</li>
    <li>Bullet point number two</li>
    <li>Bullet point number three</li>
</ul>
```

注：有些网站页面的代码没有关闭\<li> 元素，这是坏习惯

\<ul> 和\<li> 元素可以携带所有*universal*属性和*UI event*属性

##### \<ol> 元素创建有序列表

```html
<ol>
    <li>Point number one</li>
    <li>Point number two</li>
    <li>Point number three</li>
</ol>
```

可以使用 start 属性改变起始编号，不建议。

编号默认为阿拉伯数字，使用 type 属性改用字母或者罗马数字，但是不建议，建议使用 CSS。

| Value for type attribute | 效果         |
| ------------------------ | ------------ |
| 1                        | 阿拉伯数字   |
| A                        | 大写英文字母 |
| a                        | 小写英文字母 |
| I                        | 大写罗马数字 |
| i                        | 小写罗马数字 |

##### 定义列表

```html
 <dl>    
     <dt>Unordered List</dt>
     <dd>A list of bullet points.</dd>
     <dt>Ordered List</dt>
     <dd>An ordered list of points, such as a numbered set of steps.</dd>
     <dt>Definition List</dt>
     <dd>A list of terms and definitions.</dd>
</dl>
```

##### 嵌套列表

```html
<ol type="I">
    <li>Item one</li>
    <li>Item two</li>
    <li>Item three</li>
    <li>Item four
        <ol type="i">
            <li>Item 4.1</li>
            <li>Item 4.2</li>
            <li>Item 4.3</li>
        </ol>
    </li>
    <li>Item five</li>
</ol>
```

-----

### 7.Editing Text

* \<ins> 用于添加文本（常显示为下划线）
* \<del> 用于删除文本（常显示为删除线）

可以使用 title 属性标注修改人和修改理由，使用 cite 属性标注来源

datatime 属性：

YYYY-MM-DDThh:mm:ssTZD

一般是使用程序输入的

-----

### 8. 为特殊字符使用字符实体

有一些字符不能直接使用键盘输入，需要使用一些与之对应的字符来表示，称为字符实体（character entity）

转义字符（escape characters）是一种字符实体

-----

### 9. 注释

语法：

```html
<!-- comment goes here -->
```

-----

### 10. \<font> 元素（不建议使用）

调节字体

-----

### 11. 理解 Block Elements 和 Inline Elements

\<body> 内所有的 element 可以分为两类

* Block-level elements（块级元素）：显示时都以自己的新行开始

  例如：\<p>,\<hn>,\<ul>,\<ul>,\<ol>,\<dl>,\<pre>,\<hr />

* Inline elements（内联元素）：可以出现在句子中，不必出现在自己的新行中

  例如：\<b>,\<i>,\<u>,\<em>,\<strong>,\<sup>,\<sub>,\<big>,\<small>,\<ins>,\<del>,\<code>,\<dfn>,\<kbd>,\<var>

-----

### 12. Grouping Elements with \<div> and \<span>

*暂时用不到，对 CSS 有用*

##### XML 标记（The XML Declaration）

##### 文档类型声明（Document Type Declaration）

XHTML 有三种不同的风格

* Transitional XHTML 1.0
* Strict XHTML 1.0
* Frameset XHTML 1.0

为了告诉浏览器，可以使用 DOCTYPE 声明

```html
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN"
"http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
```

```html
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN"
"http://www.w3.org/TR/xhtml1/DTD/xhtml1-stirct.dtd">
```

```html
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Frameset//EN"
"http://www.w3.org/TR/xhtml1/DTD/xhtml1-frameset.dtd">
```

-----

### 13. 核心元素和属性

##### \<html>

可选的 XML 声明+必须的 DOCTYPE 声明+\<html>\</html>

如果写的是 Strict XHTML 1.0，那么 opening tag 需要包括 *namespace* ，用来明确使用的标记语言

```html
<html xmlns="http://www.w3.org/1999/xhtml">
```

**XHTML 文档应该使用 DOCTYPE 声明和 xlmns 属性指示使用的 XHTML 版本**

##### \<head>

\<head> 应该包括一个\<title> 元素，\<head> 还有可能包括的其它元素：

|           |                                 |
| --------- | ------------------------------- |
| \<base>   | 第二章                          |
| \<object> | 第三章                          |
| \<link>   | 连接到外部文件，第七章          |
| \<style>  | 把 CSS 规则包含在文档中，第七章 |
| \<script> | 把脚本包括在文档中，第十一章    |
| \<meta>   | 关键字及描述等，第十三章        |

##### \<title>

##### \<body>

-----

### 14. 属性类别

XHTML 元素可以携带三类属性

* 核心属性（Core attributes）：class，id，title，style
* Internationalization attributes：dir，lang，xml:lang
* UI events：（详见第十一章）

#### 14.1 Core attributes

##### id

唯一地标识页面中的任何元素

```html
<p id="accounts">This paragraph...</p>
<p id="sales">This paragraph...</p>
```

id 的命名规则：

> * 以字母开头，然后可以后跟任意数量的字母、数字、连字符、下划线、冒号和句号。
> * 保持唯一性，一个 XHTML 文件中没有两个 id 是一样的。

> 存在一种 "name" 属性，它有着类似的作用，适用于从前版本的 HTML 和 Transitional XHTML，在 Strict XHTML 中不可用。

##### class

指定一个元素属于一个元素类，常与 CSS 一起使用

```html
\<p class="summary">Summary goes here\</p> 
```

##### title

为元素提供建议的标题，并不是所有可以携带标题的元素都需要一个标题

```html
title="string"
```

##### style（不建议）

在元素内指定 CSS 规则

#### 14.2 Internationalization

有三个属性可以帮助用户使用不同的语言和字符编写页面，大多数 XHYML 可以使用这些属性

dir lang xml:lang

当前的浏览器对这些属性的支持是不完善的，应该尽可能指定一个字符集创建文本

有用的网址：http://www.w3.org/TR/i18n-html-tech-char/

> Internationalization 属性有时被称为 i18n 属性

##### dir

向浏览器指示文本流动的方向：从左向右或从右向左

指示整个文档的方向性的时候，应该与\<html> 元素一起使用，不同应该与\<body> 一起使用，两个原因：

* 浏览器更好的支持
* header 和 body 同时应用属性

如果希望更改文档的一小部分方向，可以对文档 body 中的元素使用 dir 属性

```html
dir="ltr"
```

默认

```html
dir="rtl"
```

阿拉伯文、希伯来文等从右向左的语言

##### lang

指示文档中使用的主要语言

只是为了兼容较早版本的 HTML，已被新 XHTML 中的 xml:lang 取代，但是建议在\<html> 元素上同时使用 lang 和 xml:lang 元素实现跨不同浏览器的兼容性

在浏览器的作用很小，但是对搜索引擎、屏幕阅读器等程序有作用

与\<html> 使用时作用于整个文档，也可以使用于其它元素使其仅作用于部分内容

ISO-639 标准双字符语言代码，方言使用破折号说明，例：

| Value | Meaning     |
| ----- | ----------- |
| ar    | Arabic      |
| en    | English     |
| en-us | U.S.English |
| zh    | Chinese     |

##### xml:lang

替代 lang，在所有的 XML 中都可用

#### 14.3 UI Events

将事件（如按键或将鼠标移动到元素上）与脚本（事件发生时运行的代码的一部分）联系起来。

在第 12 章详细了解

有十个事件，统称为 *common events*

onclick ondoubleclick onmousedown onmouseup onmouseover

onmousemove onmouseout onkeypress onkeydown onkeyup

 当页面打开或关闭时，\<body> 和\<frameset> 还具有

onload onunload

有一些事件仅适用于表单

onfocus onblur onsubmit onreset onselect onchange

### Summary