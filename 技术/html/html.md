### 初识HTML

web服务本质
```python
import socket


def main():

    sock = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
    sock.bind(('localhost', 8081))
    sock.listen(5)

    while True:
        print("server is working.....")
        conn, address = sock.accept()

        request = conn.recv(1024)
        print(request)

        conn.sendall(bytes("HTTP/1.1 201 OK\r\n\r\n<h1>Hello Yuan</h1>", "utf8"))
        conn.close()


if __name__ == '__main__':

    main()
```

html是什么
```
超文本标记语言（Hypertext Markup Language，HTML）通过标签语言来标记要显示的网页中的各个部分。一套规则，浏览器认识的规则
浏览器按顺序渲染网页文件，然后根据标记符解释和显示内容。但需要注意的是，对于不同的浏览器，对同一标签可能会有不完全相同的解释（兼容性）
静态网页文件扩展名：.html 或 .htm
```

html不是什么
```
HTML 不是一种编程语言，而是一种标记语言 (markup language)
HTML 使用标记标签来描述网页
```

html结构
```
<!DOCTYPE html>  告诉浏览器使用什么样的模式来解析当前文档
<html></html>  是文档的开始标记和结束标记。此元素告诉浏览器其自身是一个 HTML 文档，在它们之间是文档的头部<head>和主体<body>。
<head></head>  元素出现在文档的开头部分。<head>与</head>之间的内容不会在浏览器的文档窗口显示，但是其间的元素有特殊重要的意义。
<title></title>  定义网页标题，在浏览器标题栏显示。
<body></body>  之间的文本是可见的网页主体内容
```

html标签格式
```
html标签是由尖括号包围的关键词，比如<html>
html标签通常是成对出现的（双边标记），比如<div> 和 </div>
标签不区分大小写<html> 和<HTML> 推荐使用小写
标签分成两部分：开始标签<a>，结束标签</a>。两个标签中间的内容叫标签体。有些标签功能比较简单，使用一个标签就可以，这种标签叫自闭和标签。例如<br/> <hr/> <input/> <img/>
标签可以有若干个属性，也可以不带属性。如<head>元素就不带任何属性。
标签可以嵌套，但是不能交叉嵌套。<a><b><a><b>这样是错误的。

标签的语法:
<标签名 属性1="属性值1" 属性2="属性值2" ...>内容部分</标签名>
<标签名 属性1="属性值1" 属性2="属性值2" ... />
```

### 常用标签

### <!DOCTYPE>标签
```
<!DOCTYPE> 声明位于文档中的最前面的位置，处于 <html> 标签之前。此标签可告知浏览器文档使用哪种 HTML 或 XHTML 规范。
作用：声明文档的解析类型(document.compatMode)，避免浏览器的怪异模式。

document.compatMode：
    BackCompat：怪异模式，浏览器使用自己的怪异模式解析渲染页面。
    CSS1Compat：标准模式，浏览器使用W3C的标准解析渲染页面。

这个属性会被浏览器识别并使用，但是如果你的页面没有DOCTYPE的声明，那么compatMode默认就是BackCompat
```

### <head>内常用标签
#### <meta>标签
```
meta介绍
<meta>元素可提供有关页面的元信息（meta-information），针对搜索引擎和更新频度的描述和关键词。
<meta>标签位于文档的头部，不包含任何内容。
<meta>提供的信息是用户不可见的

meta标签的组成：meta标签共有两个属性，它们分别是http-equiv属性和name 属性，不同的属性又有不同的参数值，这些不同的参数值就实现了不同的网页功能。 

(1)name属性: 主要用于描述网页，与之对应的属性值为content，content中的内容主要是便于搜索引擎机器人查找信息和分类信息用的。
<meta name="keywords" content="meta总结,html meta,meta属性,meta跳转">
<meta name="description" content="老男孩培训机构是由一个很老的男孩创建的">

(2)http-equiv属性：相当于http的请求头作用，它可以向浏览器传回一些有用的信息，以帮助正确地显示网页内容，与之对应的属性值为content，content中的内容其实就是各个参数的变量值。
<meta http-equiv="Refresh" content="2;URL=https://www.oldboy.com">  // (注意后面的引号，分别在秒数的前面和网址的后面)
<meta http-equiv="content-Type" charset=UTF8">
<meta http-equiv="X-UA-Compatible" content="IE=EmulateIE7" />
```

### 非meta标签
```
<title>oldboy</title>
<link rel="icon" href="http://www.jd.com/favicon.ico">
<link rel="stylesheet" href="css.css">
<script src="hello.js"></script>
```

### <body>内常用标签
### 基本标签（块级标签和内联标签）
```
<hn>: n的取值范围是1~6; 从大到小. 用来表示标题.
<p>: 段落标签. 包裹的内容被换行.并且也上下内容之间有一行空白.
<b> <strong>: 加粗标签.
<strike>: 为文字加上一条中线.
<em>: 文字变成斜体.
<sup>和<sub>: 上角标 和 下角表.
<br>:换行.
<hr>:水平线
特殊字符：
    &lt    小于号
    &gt    大于号
    &quot    双引号
    &copy    
    &reg
```

### <div>和<span>
```
<div></div> ： <div>只是一个块级元素，并无实际的意义。主要通过CSS样式为其赋予不同的表现.
<span></span>： <span>表示了内联行(行内元素),并无实际的意义,主要通过CSS样式为其赋予不同的表现.

块级元素与行内元素的区别
所谓块元素，是以另起一行开始渲染的元素，行内元素则不需另起一行。如果单独在网页中插入这两个元素，不会对页面产生任何的影响。
这两个元素是专门为定义CSS样式而生的。
```