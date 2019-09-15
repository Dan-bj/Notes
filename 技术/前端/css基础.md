### CSS 语法
```
CSS 规则由两个主要的部分构成：1.选择器 2.一条或多条声明语句
例如：
    h1 {    // h1是选择器
        color:red;    // 声明语句，color是属性，red是值
        font-size:14px;
    }
```


### css的四种引入方式
```
1.行内式
    行内式是在标记的style属性中设定CSS样式。这种方式没有体现出CSS的优势，不推荐使用。
    <p style="background-color: rebeccapurple">Hello world</p>

2.嵌入式
    嵌入式是将CSS样式集中写在网页的<head></head>标签对的<style></style>标签对中。格式如下：
    <head>
        <meta charset="UTF-8">
        <title>Title</title>
        <style>
            p{
                background-color: #2b99ff;
            }
        </style>
    </head>

3 链接式
    将一个.css文件引入到HTML文件中
    <link href="mystyle.css" rel="stylesheet" type="text/css"/>

4.导入式
    将一个独立的.css文件引入HTML文件中，导入式使用CSS规则引入外部CSS文件，<style>标记也是写在<head>标记中，使用的语法如下：    
    <style type="text/css">
        @import"mystyle.css"; 此处要注意.css文件的路径
    </style>

注意：
    导入式会在整个网页装载完后再装载CSS文件，因此这就导致了一个问题，如果网页比较大则会儿出现先显示无样式的页面，闪烁一下之后，再出现网页的样式。这是导入式固有的一个缺陷。使用链接式时与导入式不同的是它会以网页文件主体装载前装载CSS文件，因此显示出来的网页从一开始就是带样式的效果的，它不会象导入式那样先显示无样式的网页，然后再显示有样式的网页，这是链接式的优点。
```

### css选择器
```
基本选择器
    标签选择器 p {color: red;}
    id选择器 #info {color: red;}
    class选择器 .info {color: red;}
    通配选择器 * {color: red}


组合选择器
    E, F   多元素选择器，同时匹配所有E元素或F元素，E和F之间用逗号分隔      div,p { color:#f00; }
    E F   后代元素选择器，匹配所有属于E元素后代的F元素，E和F之间用空格分隔  li a { font-weight:bold;｝
    E > F   子元素选择器，匹配所有E元素的子元素F            div > p { color:#f00; }
    E + F   毗邻元素选择器，匹配所有紧随E元素之后的同级元素F  :div + p { color:#f00; } 
    E ~ F   普通兄弟选择器（以破折号分隔）                 :.div1 ~ p{font-size: 30px; }

    注意，关于标签嵌套：
        一般，块级元素可以包含内联元素或某些块级元素，但内联元素不能包含块级元素，它只能包含其它内联元素。需要注意的是，p标签不能包含块级标签。
```