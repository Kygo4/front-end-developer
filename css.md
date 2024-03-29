# CSS

## 在HTML中使用CSS

在 HTML 中使用 CSS，包括 **内联式**、**内嵌式**、**链接式** 和 **导入式**。

-  内联式

内联式是所有样式应用方式中最为直接的一种，它通过对 HTML 标记使用 `style` 属性，将 CSS 代码直接写在其中。

```html
<!DOCTYPE html>
<html>
    <head>
        <meta charset="utf-8">
        <title>在HTML中使用CSS之内联式</title>
    </head>
    <body>
        <p style="color: #39f;">在HTML中使用CSS之内联式</p>
    </body>
</html>
```

内联式是最简单、直接的 CSS 使用方法，但它的针对性很明显，只能作用于当前标记，造成代码冗余，维护比较困难。

- 内嵌式

内嵌式与内联式使用方法不同，它将 CSS 代码写在 `<head>` 标记之间，并需要采用 `<style>` 标记进行声明。

```html
<!DOCTYPE html>
<html>
    <head>
        <meta charset="utf-8">
        <title>在HTML中使用CSS之内嵌式</title>
        <style>
            p{
                color: #39f;
            }
        </style>
    </head>
    <body>
        <p>在HTML中使用CSS之内嵌式</p>
    </body>
</html>
```

使用内嵌式 CSS 用法时 CSS 代码将被集中放在 `<head>` 标记中，这样方便查找，对后期维护比较方便，页面代码也会减少。但是，如果一个网站有很多页面，如果多个网页的某个标记要使用相同的样式效果，内嵌式也会 出现代码冗余和维护困难的问题，所以，内嵌式比较适合个别风格特殊的页面效果设置。

- 链接式

在实际的网页设计中，链接式 CSS 用法是最常用的，也是效果最好的。链接式特点是将 CSS 代码单独放在一个或多个 `.css` 文件中，实现了 CSS 代码和 HTML 代码的分离，这样使前期设计和后期维护都很方便，也有助于实现前台美工设计与后台程序设计人员的合理分工。

链接式 CSS 使用时需要在 `<head>` 标记中使用 `<link>` 标记，通过 `<link>` 标记的相关属性指明外部 CSS 文件的路径，以方便找到其中定义的 CSS 样式并运用在当前网页元素上。

```html
<!DOCTYPE html>
<html>
    <head>
        <meta charset="utf-8">
        <title>在HTML中使用CSS之链接式</title>
        <link rel="stylesheet" href="style.css">
    </head>
    <body>
        <p>在HTML中使用CSS之链接式</p>
    </body>
</html>
```

```css
@charset "utf-8";
/* CSS Document */
p{
    color: #39f;
}
```

链接式 CSS 用法的最大特点是将 CSS 代码和 HTML 代码分离，这样就可以实现将一个 CSS 文件链接到不同的 HTML 网页中。使用链接式 CSS，可以在设计整个网站时，将多个页面都会用到的 CSS 样式定义在一个或多个 `.css` 文件中，然后在需要用到该样式的 HTML 网页中通过 `<link>` 标记链接这些 `.css` 文件，通过链接式 CSS 可以降低整个网站的页面代码冗余并提高网站的可维护性。

- 导入式

导入式和链接式的用法基本相同，区别在于语法和使用方式上略有不同。导入式通过在 `<head>` 标记的 `<style>` 标记中使用 `@import` 方法导入相应的 CSS 文件。被导入的 HTML 文件在初始化时，会将该 CSS 文件导入 HTML 文件中，作为此 HTML 文件的一部分，类似于内嵌式的效果，而链接式是在 HTML 的标记需要 CSS 样式的时候才会以链接的方式引入进来。

```html
<!DOCTYPE html>
<html>
    <head>
        <meta charset="utf-8">
        <title>在HTML中使用CSS之导入式</title>
        <style>
            <!--
                @import url(style.css);
            -->
        </style>
    </head>
    <body>
        <p>在HTML中使用CSS之导入式</p>
    </body>
</html>
```
如果你网页中使用多种方式，样式之间可能会出现冲突。这时解决 CSS 冲突你就要了解在 HTML 中使用 CSS 的优先级规则：

> - 内联式 > 内嵌式 > 外部样式；
> - 在多个样式中，后出现的样式的优先级高于先出现的样式；
> - 在样式中，选择器的优先级：id 样式 > class 样式 > 标记样式。

为了避免 CSS 冲突，建议你不要混合使用多种，强力推荐使用链接式。


## CSS书写规范

> * 位置属性（`position`，`top`，`right`，`bottom`，`left`，`z-index`，`display`，`float` 等）
> * 大小（`width`，`height`，`padding`，`margin` 等）
> * 文字系列（`font`，`line-height`，`letter-spacing`，`color`，`text-align` 等）
> * 背景（`background`，`border` 等）
> * 其他（`animation`，`transition` 等）

## CSS盒子模型

![盒子模型][1]

- W3C的标准Box Model（标准 W3C 盒子模型）

```html
<!--外盒尺寸计算（元素空间尺寸）-->
Element 空间宽度 = content width + padding + border + margin
Element 空间高度 = content height + padding + border + margin
<!--内盒尺寸计算（元素大小）-->
Element Width = content width + padding + border（width 为内容宽度）
Element Height = content height + padding + border（height 为内容高度)
```

- IE传统下Box Model（IE 盒子模型）

```html
<!--外盒尺寸计算（元素空间尺寸）（占据的空间）-->
Element 空间宽度 = content width + margin (width 包含了元素内容宽度、边框宽度、内距宽度)
Element 空间高度 = content height + margin (height 包含了元素内容宽度、边框宽度、内距宽度)
<!--内盒尺寸计算（元素大小）（盒子的实际大小）-->
Element Width = content width(width 包含了元素内容宽度、边框宽度、内距宽度)
Element Height = content height(height 包含了元素内容宽度、边框宽度、内距宽度)

```

W3C 盒子模型的范围包括 `content`、`padding`、`border`、`margin`，并且 `content` 部分不包含其他部分；IE 盒子模型的范围也包括 `content`、`padding`、`border`、`margin`，和标准 W3C 盒子模型不同的是：IE 盒子模型的 `content` 部分包含了 `border` 和 `padding`。

## font-size单位

常用的有以下几种：

> - `px`：相对长度单位，相对于显示屏幕分辨率而言（像素单位）；
> - `em`：相对长度单位，相对于当前对象内文本的字体尺寸。如当前对行内文本的字体尺寸未被人为设置，则相对于浏览器的默认字体尺寸。（`em` 的值并不是固定不变的，`em` 会继承父级元素的字体大小）；
**例如**：`body` 里设置 `font-size: 100%;` 则 `16px = 1em; 12px = 0.75em; 10px = 0.625em;`。`body` 里设置 `font-size: 62.5%; 16px * 62.5% = 10px; 12px = 1.2em; 10px = 1em;`；
> - `rem`：CSS3 相对长度单位，相对于 HTML 根目录（除 IE8 及更早版本外，所有浏览器均已支持 `rem`）。
> - `pt`：磅（`1pt = 1/72 in`），标准印刷上常用的单位，一般用于页面打印排版。

绝对长度单位：`in`(英寸)、`cm`(厘米)、`mm`(毫米)、`pt`(磅)、`pc`(12点活字 1pc = 12 点)

## a伪类

```css
a:link{...}/* 未访问的链接 */
a:visited{...}/* 已访问的链接 */
a:hover{...}/* 鼠标移动到链接上 */
a:active{...}/* 选定的链接 */
```

`a:hover` 必须置于 `a:link`、`a:visited` 之后才有效，`a:active` 必须置于 `a:hover` 之后才有效。（**LVHA**）

## CSS hack

CSS hack 由于不同厂商的浏览器，比如 IE、safari、Mozilla Firefox、Chrome 等，或者是同一厂商的浏览器的不同版本，如 IE6/7。对 CSS 的解析认识完全不一样，因此会导致生成的页面效果不一样，得不到我们所需要的页面效果。这个时候我们就需要针对不同的浏览器去写不同的 CSS，让它能够同时兼容不同的浏览器。能在不同的浏览器中也能得到我们想要的页面效果。

CSS hack 的目的是使 CSS 代码兼容不同的浏览器，利用 CSS hack 为不同版本的浏览器定制编写不同的 CSS 效果。

CSS hack 有三种表现形式：**CSS 类内部 Hack**、**选择器 Hack**、**HTML 条件注释 Hack**。

- **CSS 类内部 Hack**（属性前缀法）

例如 IE6 能识别下划线 `_` 和星号 `*`，IE7 能识别星号 `*`，但不能识别下划线 `_`，IE6~IE10 都认识`\9`，但 firefox 前述三个都不能认识。

- **选择器 Hack**（选择器前缀法）

例如 IE6 能识别 `*html .class{}`，IE7 能识别 `*+html .class{}` 或者 `*:first-child + html .class{}`。

- **HTML 条件注释 Hack**（IE 条件注释法)

针对所有 IE：`<!--[if IE]><!--代码--><![endif]-->`，针对 IE6 及以下版本：`<!--[if lt IE 7]><!--代码--><![endif]-->`等等，这类 Hack 不仅对 CSS 生效，对写在判断语句里面的所有代码都会生效。

在标准模式中

> - `-` 减号是 IE6 专有的 hack
> - `\9` IE6/IE7/IE8/IE9/IE10 都生效
> - `\0` IE8/IE9/IE10 都生效，是 IE8/9/10 的 hack
> - `\9\0` 只对 IE9/IE10 生效，是 IE9/10 的 hack
> - IE7可以辨别 `*` 和 `！important`

## BFC模型（Block Formatting Contexts）

块级格式上下文，一个独立的块级渲染区域，只有 Block-level Box 参与。
浮动元素和绝对定位元素、非块级盒子的块级容器（`inline-blocks`，`table-cells`，`table-caption`）以及 `overflow` 值不为 `visiable` 的块级盒子，都会为他们创建新的 BFC（块级格式上下文）。

在 BFC 中，盒子从顶端开始垂直地一个接一个地排列。

浮动元素和绝对定位元素不与其他盒子产生外边距折叠是因为元素会脱离当前的文档流，违反了两个 `margin` 是邻接的条件的同时，又因为浮动和绝对定位使元素为它的内容创建新的 BFC。

> * 块级元素会扩展到与父元素同宽，所以块级元素会垂直排列
> * 垂直方向上的两个相邻 DIV 的 `maigin` 会重叠，而水平方向的不会（此规则并不完全正确）
> * 浮动元素会尽量接近往左上方或右上方
> * 为父元素设置 `overflow: hidden;` 或浮动父元素，则会包含浮动元素

## margin边界叠加问题

边界的高度等于两个发生叠加的边界的高度中的较大者。

解决 `margin` 边界叠加：

> * 外层 `padding`：`padding: 1px;`（或外层 `padding` 代替 `margin`）
> * 内层透明度边框：`border: 1px solid transparent;`
> * 内层绝对定位： `position: absolute;`
> * 外层 DIV：`overflow: hidden;`
> * 内层 DIV：`float: left; display: inline;`
> * 外层 DIV：`zoom: 1;`

## position属性值

> * `absolute`：生成绝对定位的元素，相对于 `static` 定位以外的第一个父元素进行定位。（整个元素飘出文档流，而且元素自身的物理空间也同时消失。）
> * `fixed`：生成绝对定位的元素，相对于浏览器窗口进行定位。
> * `relative`：生成相对定位的元素，相对于其正常位置进行定位。（物理空间依然存在，相对定位不影响其他相邻的元素。）
> * `static`：默认值，没有定位。元素出现在正常的流中。（忽略 `top`、`right`、`bottom`、`left` 或者 `z-index`）
> * `inherit`：规定应该从父元素继承 `position` 属性的值。

## display属性值

|值|描述|
| --------   | :----:  |
|`none`|此元素不会被显示。|
|`block`|此元素将显示为块级元素，此元素前后会带有换行符。|
|`inline`|默认。此元素会被显示为内联元素，元素前后没有换行符。|
|`inline-block`|行内块元素。（CSS2.1 新增的值）|
|`list-item`|此元素会作为列表显示。|
|`run-in`|此元素会根据上下文作为块级元素或内联元素显示。|
|`compact`|CSS 中有值 `compact`，不过由于缺乏广泛支持，已经从 CSS2.1 中删除。|
|`marker`|CSS 中有值 `marker`，不过由于缺乏广泛支持，已经从 CSS2.1 中删除。|
|`table`|此元素会作为块级表格来显示（类似 `<table>`），表格前后带有换行符。|
|`inline-table`|此元素会作为内联表格来显示（类似 `<table>`），表格前后没有换行符。|
|`table-row-group`|此元素会作为一个或多个行的分组来显示（类似 `<tbody>`）。|
|`table-header-group`|此元素会作为一个或多个行的分组来显示（类似 `<thead>`）。|
|`table-footer-group`|此元素会作为一个或多个行的分组来显示（类似 `<tfoot>`）。|
|`table-row`|此元素会作为一个表格行显示（类似 `<tr>`）。|
|`table-column-group`|此元素会作为一个或多个列的分组来显示（类似 `<colgroup>`）。|
|`table-column`|此元素会作为一个单元格列显示（类似 `<col>`）。|
|`table-cell`|此元素会作为一个表格单元格显示（类似 `<td>` 和 `<th>`）。|
|`table-caption`|此元素会作为一个表格标题显示（类似 `<caption>`）。|
|`inherit`|规定应该从父元素继承 `display` 属性的值。|

## 左边固定右边自适应

```css
/* 第一种 */
.left{
    float: left;
    width: 100px;
}
.right{
    margin-left: 100px;
}
/* 第二种 */
.left{
    position: absolute;
    top: 0;
    left: 0;
    width: 100px;
}
.right{
    margin-left: 100px;
}
/* 第三种 */
.container{/* .left 和 .right 的父级 */
    display: table;
}
.left{
    display: table-cell;
    width: 100px;
}
.right{
    display: table-cell;
}
```

## 右边固定左边自适应

```css
/* 第一种 */
/* 局限性：HTML 中先 right，后 left */
.left{
    margin-right: 100px;
}
.right{
    float: right;
    width: 100px;
}
/* 第二种 */
.left{
    margin-right: 100px;
}
.right{
    position: absolute;
    top: 0;
    right: 0;
    width: 100px;
}
/* 第三种 */
.container{/* .left 和 .right 的父级 */
    display: table;
}
.left{
    display: table-cell;
}
.right{
    display: table-cell;
    width: 100px;
}
```

## 两边固定中间自适应

```css
/* 第一种 */
/* 局限性：HTML 中先 left，后 right，再 center */
.left{
    float: left;
    width: 100px;
}
.center{}
.right{
    float: right;
    width: 100px;
}
/* 第二种 */
.left{
    position: absolute;
    top: 0;
    left: 0;
    width: 100px;
}
.center{
    margin: 0 100px;
}
.right{
    position: absolute;
    top: 0;
    right: 0;
    width: 100px;
}
/* 第三种 */
/* 局限性：HTML 中先 center，后 left，再 right */
.container{/* .left、.center 和 .right 的父级 */
    padding: 0 100px;
    *overflow: hidden;
}
.center{
    float: left;
    width: 100%;
}
.left,.right{
    position: relative;
    _display: inline;
 }
.left{
    right: 100px;
    float: left;
    width: 100px;
    margin-left: -100%;
    _right: -200px;
}
.right{
    float: right;
    width: 100px;
    margin-right: -100px;
}
/* 第四种 */
.container{/* .left、.center 和 .right 的父级 */
    display: table;
}
.left,.right{
    display: table-cell;
    width: 100px;
}
.center{
    display: table-cell;
}
```

## 中间固定两边自适应

```css
/* 第一种 */
.left,.right{
    float: left;
    width: 50%;
    margin-left: -50px;
}
.left .inner,.right .inner{/* 加一层 DIV */
    margin-left: 50px;
}
.center{
    float: left;
    width: 100px;
}
/* 第二种 */
/* CSS3 Flexbox */
.container{
    display: -webkit-flex;
    display: -moz-flex;
    display: -o-flex;
    display: -ms-flex;
    display: flex;
}
.left,.right{
    flex: 1;
}
.center{
    width: 100px;
}
```

## 不换行，文本超出指定宽度后省略号代替

```css
li{
    display: block;/* 内联元素需加 */
    width: 200px;
    word-break: keep-all;/* 不换行 */
    white-space: nowrap;/* 不换行 */
    overflow: hidden;/* 内容超出宽度时隐藏超出部分的内容 */
    text-overflow: ellipsis;/* 省略号 */
}
```

## 水平居中

> - `margin: 0 auto;` 与 `text-align: center;`
> - 相对定位 `position: relative;` 与负的边距 `margin-left`

更多方法：[六种实现元素水平居中][2]

## 垂直居中

```css
/* 第一种 */
.div{
    width: 100%;
    height: 200px;
    line-height: 200px;
}
/* 第二种 */
.parent{
    display: table;
}
.child{
    display: table-cell;
    vertical-align: middle;
}
/* 第三种 */
.parent{
    position: relative;
}
.child{
    position: absolute;
    top: 50%;
    left: 50%;
    width: 50%;
    height: 30%;
    margin: -15% 0 0 -25%;
}
/* 第四种 */
.parent{
    position: relative;
}
.child{
    position: absolute;
    top: 0;
    right: 0;
    bottom: 0;
    left: 0;
    width: 50%;
    height: 30%;
    margin: 0 auto;
}
/* 第五种 */
.parent{
    padding: 5% 0;
}
.child{
    padding: 10% 0;
}
/* 第六种 */
.parent{
    height: 250px;
}
.floater{
    float: left;
    width: 100%;
    height: 50%;
    margin-bottom: -50px;
}
.child{
    clear: both;
    height: 100px;
}
```

## 清除浮动

```css
/* 第一种 增加额外一个元素 */
.clear{
    clear: both;
    /* IE */
    height: 0;
    font-size: 0;
    line-height: 0;
}
/* 第二种 overflow */
.parent{
    overflow: auto;
    zoom: 1;/* 缩放比例，兼容 IE */
}
/* 或者 */
.parent{
    0\ overflow: auto;/* 除 IE5/6 */
}
* html .parent{
    height: 1%;/* IE5/6 */
}
/* 第三种 伪元素：before、:after */
.parent:before,.parent:after{
    content: ".";
    display: block;
    height: 0;
    visibility: hidden;
}
.parent:after{
    clear: both;
}
.parent{
    zoom: 1;/* IE < 8 */
}
/* 或者 */
.parent:before,.parent:after{
    content: " ";
    display: table;
}
.parent:after{
    clear: both;
    overflow: hidden;
}
.parent{
    zoom: 1;/* IE < 8 */
}
```

## 隐藏元素

```css
/* 第一种 */
.div{/* 不占据空间，无法点击 */
    display: none;
}
/* 第二种 */
.div{/* 占据空间，无法点击 */
    visibility: hidden;
}
/* 第三种 */
.div{/* 不占据空间，无法点击 */
    position: absolute;
    top: -999em;
}
/* 第四种 */
.div{/* 占据空间，无法点击 */
    position: relative;
    top: -999em;
}
/* 第五种 */
.div{/* 不占据空间，无法点击 */
    position: absolute;
    visibility: hidden;
}
/* 第六种 */
.div{/* 不占据空间，无法点击 */
    overflow: hidden;
    height: 0;
}
/* 第七种 */
.div{/* 占据空间，可以点击 */
    opacity: 0;
    filter:Alpha(opacity=0);
}
/* 第八种 */
.div{/* 不占据空间，可以点击 */
    position: absolute;
    opacity: 0;
    filter:Alpha(opacity=0);
}
/* 第九种 */
.div{
    /* IE6/IE7/IE9 不占据空间 */
    /* IE8/firefox/Chrome/Opera 占据空间 */
    /* 都无法点击 */
    zoom: 0.001;
    -webkit-transform: scale(0);
    -moz-transform: scale(0);
    -o-transform: scale(0);
    transform: scale(0);
}
/* 第十种 */
.div{/* 不占据空间，无法点击 */
    position: absolute;
    zoom: 0.001;
    -webkit-transform: scale(0);
    -moz-transform: scale(0);
    -o-transform: scale(0);
    transform: scale(0);
}
```


  [1]: https://github.com/bizhongbio/front-end-developer/blob/master/images/box-model.png
  [2]: http://www.w3cplus.com/css/elements-horizontally-center-with-css.html