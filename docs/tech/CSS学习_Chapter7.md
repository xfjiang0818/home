# Chapter 7 Cascading Style Sheets

学习内容：

* CSS 规则的构成
* 如何在文档中放置 CSS 规则以及如何链接到外部 CSS 文档
* 属性和值如何控制文档中不同元素的显示
* 如何使用 CSS 控制文本的显示
* CSS 如何基于 box 模型，以及如何为这些 box 设置不同的属性



## 1. Introducing CSS

CSS 规则由两部分组成：

* *selector* 指示应用于哪个或哪些元素，应用于多个时，使用逗号分隔
* *declaration* 规定如何设置 *selector* 选择的样式

```css
td {width:36px;}
```

declaration 也分为两个部分：

* *property* 选择想要影响的 element(s)
* *value* 是 property 的规范

举例如下

```css
h1, h2, h3 {
    font-weight:bold;
    font-family:arial;
    color:#000000;
    background-color:#FFFFFF;
}
```

CSS 规则可以存在于 XHTML 文档中，也可以存在于单独的文件中，同时 XHTML 包含到这个 *style sheet* 文件的链接

XHTML：

```html
<?xml version="1.0" encoding="iso-8859-1"?>
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN"
    "http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd">
<html xmlns="http://www.w3.org/1999/xhtml" lang="en">
<head>
    <title>CSS Example</title>
    <link rel="stylesheet" type="text/css" href="ch07_eg01.css" />
</head>
<body>
    <h1>Basic CSS Font Properties</h1>
    <p>The following table shows you the basic CSS font 
        properties that allow you to change the appearance of 
        text in your document.</p>
    <table>
        <tr>
            <th>Property</th>
            <th>Purpose</th>
        </tr>
        <tr>
            <td class="code">font-family</td>
            <td>Specifies the font used.</td>
        </tr>
        <tr>
            <td class="code">font-size</td>
            <td>Specifies the size of the font used.</td>
        </tr>
        <tr>
            <td class="code">font-style</td>
            <td>Specifies whether the font should be 
                normal, italic or oblique.</td>
        </tr>
        <tr>
            <td class="code">font-weight</td>
            <td>Specifies whether the font should be 
                normal, bold, bolder, or lighter</td>
        </tr>
    </table>
</body>
</html>
```

CSS：

```css
/* Style sheet for ch07_eg01.html */
```

/* 和 */ 之间的内容会被无视掉，并且不会对页面的外观产生影响

```css
body {
    color:#000000;
    background-color:#ffffff;
    font-family:arial, verdana, sans-serif;
}
```

第一个规则应用于 \<body> 元素，在指定的页面上使用的任何文本和行的默认颜色是黑色，并且页面的背景应该是白色的。颜色使用十六进制代码表示。整个文件的字体是 Arial ，如果没有，就用 Verdana 字体；否则，将使用默认字体组。

```css
h1 {font-size:18pt;}
p {font-size:12pt}
```

设定字体大小

```css
table {
    back-ground-color:#efefef;
    border-style:solid;
    border-width:1px;
    border-color:#999999;
}
```

设定表格的背景为灰色，加上一个边框。边框是 solid 而不是 dashed 或 dotted 的。边框有 1 pixel 厚，颜色为 light grey 

```css
th {
    background-color:#cccccc;
    font-weight:bold;
    padding:5px;
}
```

表格标题的背景为中灰色，文本以粗体显示，在单元格边缘和文本之间有 5 个像素的 *padding* 填充

```css
td {padding:5px;}
```

各个表格数据单元格还具有5个填充像素

```css
td.code {
    font-family:courier, courier-new, serif;
    font-weight:bold;
}
```

为所有 class="code" 的元素设定字体



### Inheritance

 CSS 的强大功能之一是当一个 property 被应用到一个 element 之后，这个 element 中包含的所有子元素都会继承这个规则

如果另一个规则更具体地说明它应用于哪些元素，那么它将覆盖之前的属性

具体的属性详见附录C



## 2. Where You Can Add CSS Rules

* 可以放在外部

* 也可以放在内部的两个地方：
  * \<style> 元素内，它位于文档的 \<head> 元素中
  * 作为 style 属性的值，这对于所有可携带 style 属性的元素都适用

当样式表规则保存在文档头部的 \<style> 元素中时，称为一个 *internal style sheet*，例：

```html
<head>
    <title>Internal Style sheet</title>
    <style type="text/css">
        body {
            color:#000000;
            background-color:#ffffff;
            font-family:arial, verdana, sans-serif;
        }
        h1 {font-size:18pt;}
        p {font-size:12pt;}
    </style>
</head>
```

当 XHTML 元素使用 style 属性的时候，称为 *inline style rules*，例：

```html
<td style="font-family:courier; padding:5px; border-style:solid;
           border-width:1px; border-color:#000000;">
```

>  不建议使用 style 属性，违背了 XHTML 只负责标记结构的原则



### \<link> 元素

用来描述两个文档之间的关系。例如，可以使用它来指定页面使用的 style sheet。也可以有其他的用途，例如指定页面相对应的 RSS 提要

这种来链接与 \<a> 非常不同，因为不需要点击什么来激活，它自动相关联

\<link> 元素始终是空元素，它与 style sheet 一起使用时，必须有三个属性：type，ref 和 href

```css
<link rel="stylesheet" type="text/css" href="../CSS/interface.css" />
```

各种属性：

#### *rel*

必需，指定包含连接的文档与被链接的文档之间的关系

```html
rel="stylesheet"
```

#### *type*

指定链接道德文档的 MIME 类型。处理 CSS 表时的类型为 text/css

```html
type="text/css"
```

#### *href*

指定链接到的文档的 URL，可以是绝对 URL 也可以是相对 URL

```html
href="../stylesheet/interface.css"
```

#### *hreflang*

指定写入指定资源的语言。在使用时，它的值是附录G中之一

```html
hreflang="en-US"
```

#### *media*

指定文档的输出设备

```html
media="screen"
```

不常使用，在使用稀奇古怪的设备访问网页时可能会用到



### \<style> 元素

\<style> 元素使用于 \<head> 元素中，在 web 页面中包含样式表规则而不是链接到外部。

当一个页面需要包含一些额外的规则，而这些规则并不适用于所用共享样式的站点的其它页面时，有时会用到。

```html
<head>
    <title>
        <link rel="stylesheet" type="text/css" href="../styles/mySite.css" />
        <style type="text/css">
            h1 {color:#FF0000;}
        </style>
    </title>
</head>
```

type 是必带属性，还可以携带：dir，lang，media，title，type



### External CSS Style Sheets 的优点

* 就写一次，省劲儿
* 好改
* 浏览器会保存 CSS 样式表的副本，在访问第一页的时候会下载，后面几页的访问速度会加快，同时减小了服务器的压力
* 作为模板
* 同一文档使用不同的样式表
* 样式表相互导入
* 删除样式表更适合视觉障碍者使用



## 3. CSS Properties

查表



## 4. Controlling Text

控制文档中文本外观的属性可分为两组

* 直接影响字体和外观的
* 对所有字体都有影响的，例如颜色、间距

| Property         | Purpose                   |
| ---------------- | ------------------------- |
| font             | 将下面几个属性结合成一个  |
| font-family      |                           |
| font-size        |                           |
| font-weight      | normal or bold            |
| font-style       | normal, italic or oblique |
| font-strecth     | 控制字体中实际字符的宽度  |
| font-variant     | 普通字体/小写字体         |
| font-size-adjust | 字体大小，宽高比          |

font 不同于 typeface

* typeface 是 font 的家族，比如 Arial
* font 是家族中的具体成员，比如 Arial 12-point bold

typeface 分为两类

* serif 衬线字体
* sans-serif 无衬线字体

> monospace 等宽字体
>
> non-monospace 不等宽字体 

衬线字体适合印刷，无衬线字体适合网络，因为屏幕的分辨率不如打印出来的文档

### 4.1 The font-family Property

### 4.2 The font-size Property

### 4.3 The font-weight Property

### 4.4 The font-style Property

### 4.5 The font-variant Property

### 4.6 The font-stretch Property

### 4.7 The font-size-adjust Property



## 5. Text Formatting

除了影响 font 的属性，影响外观的其它属性

| Property        | Purpose                              |
| --------------- | ------------------------------------ |
| color           |                                      |
| text-align      | 文本在包含它的元素内的水平对齐方式   |
| vertical-align  | 文本在包含它的元素内的垂直对齐方式   |
| text-decoration | 是否加下划线、横线、删除线、闪烁文本 |
| text-indent     | 从左边框缩进                         |
| text-transform  | 指定内容为全部大写、小写             |
| text-shadow     | 阴影                                 |
| letter-spacing  | 字母间的宽度                         |
| word-spacing    | 单词之间的空间                       |
| white-space     | 是否应该折叠、保留或防止包装空白     |
| direction       | 指定文本的方向（类似于 dir 属性）    |



## 6. Text Pseudo-Classes

有两个伪类可以帮助处理文本，允许以与元素其余部分不同的方式呈现元素的第一个字母或第一行



### 6.1 The first-letter Pseudo-Class

仅为元素的首字母指定规则，在某些杂志文章或书籍中常用于新页面的第一个字符

```css
p.introduction:first-letter {font-size:42px;}
```

应用于 p 元素首字母



### 6.2 The first-line Pseudo-Class

第一行，值得注意的是这个第一行是真的第一行，无论浏览器一行显示多少

```css
p.introduction:first-line {font-weight:bold;}
```



## 7. Selectors

各种各样的选择器

### Universal Selector

### The Type Selector

### The Class Selector

### The ID Selector

### The Child Selector

### The Descendant Selector

### The Adjzcent Sibling Selector

### The General Sibling Selector

###   Using Child and Sibling Selectors To Reduce Dependence on Classes in Markup

### Attribute Selectors



## 8. Lengths

CSS 中指定长度的三种方式

* Relative units
* Absolute units
* Percentages

### Relative Units

#### px

#### em

#### ex

### Absolute Units

### Percentages



## 9. Introducing the Box Model

*box* 模型是 CSS 中非常重要的概念，决定了元素在浏览器窗口中的位置，名字源于 CSS 将每个元素都当作在一个 box 中

| Property | Description                      |
| -------- | -------------------------------- |
| border   |                                  |
| margin   | 两个 box 的 border 之间的距离    |
| padding  | box 里的内容到 border 之间的距离 |

margin 的有趣问题：两个 margin 相遇时只会显示较大的那个

