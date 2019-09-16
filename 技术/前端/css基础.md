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


属性选择器
    E[att]          匹配所有具有att属性的E元素，不考虑它的值。（注意：E在此处可以省略。比如“[cheacked]”。以下同。）
                    p[title] { color:#f00; }

    E[att=val]      匹配所有att属性等于“val”的E元素
                    div[class=”error”] { color:#f00; }

    E[att~=val]     匹配所有att属性具有多个空格分隔的值、其中一个值等于“val”的E元素
                    td[class~=”name”] { color:#f00; }
 
    E[attr^=val]    匹配属性值以指定值开头的每个元素                    
                    div[class^="test"]{background:#ffff00;}
 
    E[attr$=val]    匹配属性值以指定值结尾的每个元素
                    div[class$="test"]{background:#ffff00;}
 
    E[attr*=val]    匹配属性值中包含指定值的每个元素
                    div[class*="test"]{background:#ffff00;}



伪类
    anchor伪类：专用于控制链接的显示效果
        a:link（没有接触过的链接）,用于定义了链接的常规状态。

        a:hover（鼠标放在链接上的状态）,用于产生视觉效果。
        
        a:visited（访问过的链接）,用于阅读文章，能清楚的判断已经访问过的链接。
        
        a:active（在链接上按下鼠标时的状态）,用于表现鼠标按下时的链接状态。
        
        伪类选择器 : 伪类指的是标签的不同状态:
        
            a ==> 点过状态 没有点过的状态 鼠标悬浮状态 激活状态
        
        a:link {color: #FF0000} /* 未访问的链接 */
        
        a:visited {color: #00FF00} /* 已访问的链接 */
        
        a:hover {color: #FF00FF} /* 鼠标移动到链接上 */
        
        a:active {color: #0000FF} /* 选定的链接 */ 格式: 标签:伪类名称{ css代码; }

    <!DOCTYPE html>
    <html lang="en">
        <head>
            <meta charset="UTF-8">
            <title>Title</title>
            <style>
                .top{
                    background-color: rebeccapurple;
                    width: 100px;
                    height: 100px;
                }
                .bottom{
                    background-color: green;
                    width: 100px;
                    height: 100px;
                }

                .outer:hover .bottom{
                    background-color: yellow;
                }

                注意:一定是outer:hover  控制outer里某一个标签,否则无效

                .top:hover .bottom{
                    background-color: yellow;
                }
            </style>
        </head>
        <body>
            <div class="outer">
                <div class="top">top</div>
                <div class="bottom">bottom</div>
            </div>
        </body>
    </html>


before after伪类 
    :before    p:before       在每个<p>元素之前插入内容     
    :after     p:after        在每个<p>元素之后插入内容     

    例：p:before{content:"hello";color:red;display: block;}



选择器的优先级　
    css的继承
        继承是CSS的一个主要特征，它是依赖于祖先-后代的关系的。继承是一种机制，它允许样式不仅可以应用于某个特定的元素，还可以应用于它的后代。例如一个BODY定义了的颜色值也会应用到段落的文本中。
        
        body{color:red;}       <p>helloyuan</p>
        这段文字都继承了由body {color:red;}样式定义的颜色。然而CSS继承性的权重是非常低的，是比普通元素的权重还要低的0。

        p{color:green}
        发现只需要给加个颜色值就能覆盖掉它继承的样式颜色。由此可见：任何显示申明的规则都可以覆盖其继承样式。

        此外，继承是CSS重要的一部分，我们甚至不用去考虑它为什么能够这样，但CSS继承也是有限制的。有一些属性不能被继承，如：border, margin, padding, background等。
        div{
            border:1px solid #222
        }

        <div>
            hello
            <p>yuan</p>
        </div>
    

    css的优先级
        所谓CSS优先级，即是指CSS样式在浏览器中被解析的先后顺序。


        样式表中的特殊性描述了不同规则的相对权重，它的基本规则是：
            1 内联样式表的权值最高             style=""－－－－－－－－－－－－ 1000；
            2 统计选择符中的ID属性个数。       #id －－－－－－－－－－－－－－ 100
            3 统计选择符中的CLASS属性个数。    .class －－－－－－－－－－－－－ 10
            4 统计选择符中的HTML标签名个数。    p －－－－－－－－－－－－－-－ 1
            按这些规则将数字符串逐位相加，就得到最终的权重，然后在比较取舍时按照从左到右的顺序逐位比较。


        1. 文内的样式优先级为1,0,0,0，所以始终高于外部定义。
        2. 有!important声明的规则高于一切。
        3、如果!important声明冲突，则比较优先权。
        4、如果优先权一样，则按照在源码中出现的顺序决定，后来者居上。
        5、由继承而得到的样式没有specificity的计算，它低于一切其它规则(比如全局选择符*定义的规则)。
```