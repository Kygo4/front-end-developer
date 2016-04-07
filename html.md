# HTML


## 对WEB标准以及W3C的理解与认识

WEB标准不是某一个标准，而是一系列标准的集合。网页主要由三部分组成：结构（Structure）、表现（Presentation）和行为（Behavior）。对应的标准也分三方面：结构化标准语言主要包括XHTML和XML，表现标准语言主要包括CSS，行为标准主要包括对象模型（如W3C DOM）、ECMAScript等。这些标准大部分由万维网联盟（外语缩写：W3C）起草和发布，也有一些是其他标准组织制订的标准，比如ECMA（European Computer Manufacturers Association）的ECMAScript标准。

> - web标准规范要求，书写标签必须闭合、标签小写、不乱嵌套，可提高搜索机器人对网页内容的搜索几率（SEO）；

> - 建议使用外链css和js脚本，从而达到结构与行为、结构与表现的分离，提高页面的渲染速度，能更快地显示页面的内容；

> - 样式与标签的分离，更合理的语义化标签，使内容能被更多的用户所访问、内容能被更广泛的设备所访问、更少的代码和组件，从而降低维护成本、改版更方便；

> - 不需要变动页面内容，便可提供打印版本而不需要复制内容，提高网站易用性。

遵循w3c制定的web标准，能够使用户浏览者更方便的阅读，使网页开发者之间更好的交流。

## HTML与XHTML有什么差别

HTML与XHTML之间的差别，粗略可以分为两大类比较：一个是功能上的差别，另外是书写习惯的差别。关于功能上的差别，主要是XHTML可兼容各大浏览器、手机以及平板，并且浏览器也能快速正确地编译网页。

HTML是一种基本的WEB网页设计语言，XHTML是一个基于XML的标记语言。

> * XHTML元素必须被正确地嵌套
> * XHTML元素必须被关闭
> * 标签名必须用小写字母
> * XHTML文档必须拥有根元素

**XHTML的规则**

- 所有标签都必须小写

在XHTML中，所有的标签都必须小写，不能大小写穿插其中，也不能全部都是大写。看一个例子。

```html
错误：<Head></Head><Body></Body>
正确：<head></head><body></body>
```

- 标签必须成双成对

像是p、a、div标签等，当出现一个标签时，必须要有对应的结束标签，缺一不可，就像在任何程序语言中的括号一样。

```html
错误：大家好<p>我是muki
正确：<p>大家好</p><p>我是muki</p>
```

- 标签顺序必须正确

标签由外到内，一层层包覆着，所以假设你先写div后写h1，结尾就要先写h1后写div。只要记住一个原则“先进后出”，先弹出的标签要后结尾。

```html
错误：<div><h1>大家好</div></h1>
正确：<div><h1>大家好</h1></div>
```

- 所有属性都必须使用双引号

在XHTML 1.0中规定连单引号也不能使用，所以全程都得用双引号。

```html
错误：<div style=font-size:11px>hello</div>
正确：<div style="font-size:11px">hello</div>
```

- 不允许使用target="_blank"

从XHTML 1.1开始全面禁止target属性，如果想要有开新窗口的功能，就必须改写为rel="external"，并搭配JavaScript实现此效果。

```html
错误：<a href="http://blog.mukispace.com" target="_blank">MUKI space</a>
正确：<a href="http://blog.mukispace.com" rel="external">MUKI space</a>
```

## Doctype? 严格模式与混杂模式-如何触发这两种模式，区分它们有何意义?

混杂模式是一种比较宽松的向后兼容的模式。混杂模式通常模拟老式浏览器的行为，以防止老站点无法工作 。

|模式|作用|
| --------   | :----:  |
| 混杂模式（quirks mode）|让IE的行为与（包含非标准特性的）IE5相同|
| 标准模式（standards mode）|让IE的行为更接近标准行为|
| 准标准模式（almost standards mode）|这种模式下的浏览器特性有很多都是符合标准的，不标准的地方主要体现在处理图片间隙的时候（在表格中使用图片时问题最明显）|
| 超级标准模式|IE8引入的一种新的文档模式，超级文档模式可以让IE以其所有版本中最符合标准的方式来解释网页内容|

**触发混杂模式**: 如果在文档开始处没有发现文档类型声明，则所有浏览器都会默认开启混杂模式。但采用混杂模式不是什么值得推荐的做法，因为不同浏览器在这种模式下的行为差异非常大，如果不使用某些hack技术，跨浏览器的行为根本就没有一致性可言。

根据Doctype是否存在以及使用哪种DTD来触发其不同的模式。如果Doctype不存在或者其形式不正确那么默认为混杂模式。如果XHTMLl文档中包含完整的Doctype，那么它一般以标准模式呈现。 

区分它们的意义可以让开发者更好的写出标准兼容的页面，同时不影响以前的页面标准。

## 行内元素、块级元素有哪些？

```html
<!--块元素(block element)HTML标签分类明细-->

    * address - 地址 
    * blockquote - 块引用 
    * center - 居中中对齐块 
    * dir - 目录列表 
    * div - 常用块级容易，也是css layout的主要标签 
    * dl - 定义列表 
    * fieldset - form控制组 
    * form - 交互表单 （只能用来容纳其它块元素） 
    * h1 - 大标题 
    * h2 - 副标题 
    * h3 - 3级标题 
    * h4 - 4级标题 
    * h5 - 5级标题 
    * h6 - 6级标题 
    * hr - 水平分隔线 
    * isindex - input prompt 
    * menu - 菜单列表 
    * noframes - frames可选内容，（对于不支持frame的浏览器显示此区块内容 
    * noscript - 可选脚本内容（对于不支持script的浏览器显示此内容） 
    * ol - 排序表单 
    * p - 段落 
    * pre - 格式化文本 
    * table - 表格 
    * ul - 非排序列表

<!--内联元素(inline element)HTML标签分类明细-->

    * a - 锚点 
    * abbr - 缩写 
    * acronym - 首字 
    * b - 粗体(不推荐) 
    * bdo - bidi override 
    * big - 大字体 
    * br - 换行 
    * cite - 引用 
    * code - 计算机代码(在引用源码的时候需要) 
    * dfn - 定义字段 
    * em - 强调 
    * font - 字体设定(不推荐) 
    * i - 斜体 
    * img - 图片 
    * input - 输入框 
    * kbd - 定义键盘文本 
    * label - 表格标签 
    * q - 短引用 
    * s - 中划线(不推荐) 
    * samp - 定义范例计算机代码 
    * select - 项目选择 
    * small - 小字体文本 
    * span - 常用内联容器，定义文本内区块 
    * strike - 中划线 
    * strong - 粗体强调 
    * sub - 下标 
    * sup - 上标 
    * textarea - 多行文本输入框 
    * tt - 电传文本 
    * u - 下划线 
    * var - 定义变量

<!--可变元素HTML标签分类明细-->

    * applet - java applet　　 
    * button - 按钮　　 
    * del - 删除文本　　 
    * iframe - inline frame　　 
    * ins - 插入的文本　　 
    * map - 图片区块(map)　　 
    * object - object对象　　 
    * script - 客户端脚本
```

## 行内元素与块级元素不同点

块级元素和行内元素的区别是，块级元素会占一行显示，而行内元素可以在一行并排显示。通过样式控制，它们可以相互转换。

块级元素和行内元素之间的一个重要的不同点：尺寸。

> * 设置宽度width无效
> * 设置高度height无效，可以通过line-height来设置
> * 设置margin只有左右margin有效，上下无效
> * 设置padding只有左右padding有效，上下则无效

**注**：无效指它对其它元素的排列没有影响。也就是说，对于设置的margin,padding行内元素文档流里的上下元素来说，他们的间距不会因为上下margin或者上下padding而产生间距。但是就他本身而言，对于上下margin与padding是有效的。
