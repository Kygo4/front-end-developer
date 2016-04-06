# JavaScript

## JavaScript实现

一个完整的 JavaScript 实现由核心（ECMAScript）、文档对象模型（DOM）、浏览器对象模型（BOM）三部分组成。

- **ECMAScript**：由 ECMA-262 定义的 ECMAScript 与 Web 浏览器没有依赖关系。ECMA-262 规定了这门语言的组成部分有语法、类型、语句、关键字、保留字、操作符和对象。ECMAScript 就是对实现该标准规定的各个方面内容的语言的描述。**（由 ECMA-262 定义，提供核心语言功能。）**
- **文档对象模型（DOM）**：文档对象模型（DOM，Document Object Model）是针对 XML 但经过扩展用于 HTML 的应用程序编程接口（API，Application Programming Interface）。**（提供访问和操作网页内容的方法和接口。）**
- **浏览器对象模型（BOM）**：浏览器对象模型（BOM，Browser Object Model）支持可以访问和操作浏览器窗口。开发人员使用 BOM 可以控制浏览器显示的页面以外的部分。**（提供与浏览器交互的方法和接口。）**

## `<script>`元素

把 JavaScript 插入到 HTML 页面中要使用 `<script>` 标签。使用这个元素可以把 JavaScript 嵌入到 HTML 页面中，让脚本与标记混合在一起；也可以包含外部的 JavaScript 文件。而我们需要注意的地方有：

- 在包含外部 JavaScript 文件时，必须将 src 属性设置为指向相应文件的 URL。而这个文件既可以是与包含它的页面位于同一个服务器上的文件，也可以是其他任何域中的文件。
- 所有 `<script>` 元素都会按照它们在页面中出现的先后顺序依次被解析。在不使用 `defer` 和 `async` 属性的情况下，只有在解析完前面 `<script>` 元素的代码之后，才会开始解析后面 `<script>` 元素中的代码。
- 由于浏览器会先解析完不使用 `defer` 属性的 `<script>` 元素中的代码，然后再解析后面的内容，所以一般应该把 `<script>` 元素放在页面最后，即主要内容后面，`</body>` 标签前面。
- 使用 `defer` 属性可以让脚本在文档完全呈现之后再执行。延迟脚本总是按照指定它们的顺序执行。
- 使用 `async` 属性可以表示当前脚本不必等待其他脚本，也不必阻塞文档呈现。不能保证异步脚本按照它们在页面中出现的顺序执行。

另外，使用 `<noscript>` 元素可以指定在不支持脚本的浏览器中显示的替代内容。但在启用了脚本的情况下，浏览器不会显示 `<noscript>` 元素中的任何内容。

## 标识符

所谓标识符，就是指变量、函数、属性的名字，或者函数的参数。标识符可以是按照下列格式规则组合起来的一或多个字符：
> - 第一个字符必须是一个字母、下划线（_）或一个美元符号（$）;
> - 其他字符可以是字母、下划线、美元符或数字。

标识符中的字母也可以包含扩展的 ASCII 或 Unicode 字母字符，但我们不推荐这样做。

按照惯例，ECMAScript 标识符采用 **驼峰大小写格式**，也就是第一个字母小写，剩下的每个单词的首字母大写。**（为了与 ECMAScript 内置的函数和对象命名格式保持一致）**

## 关键字和关键字

- 关键字

ECMA-262 描述了一组具有特定用途的关键字，这些关键字可用于表示控制语句的开始或结束，或者用于执行特定操作等。按照规则，关键字也是语言保留的，不能用作标识符。以下就是 ECMAScript 的全部关键字（带* * 号上标的是第 5 版新增的关键字）：

> - break
> - case
> - catch
> - continue
> - debugger*
> - default
> - delete
> - do
> - else
> - finally
> - for
> - function
> - if
> - in
> - instanceof
> - new
> - return
> - switch
> - this
> - throw
> - try
> - typeof
> - var
> - void
> - while
> - with

- 保留字

ECMA-262 描述了一组具有特定用途的关键字外，还描述了另外一组不能用作标识符的保留字。尽管保留字在这门语言中还没有任何特定的用途，但它们有可能在将来被用作关键字。以下是 ECMA-262 第 3 版定义的全部保留字：

> - abstract
> - boolean
> - byte
> - char
> - class
> - const
> - debugger
> - double
> - enum
> - export
> - extends
> - final
> - float
> - goto
> - implements
> - import
> - int
> - interface
> - long
> - native
> - package
> - private
> - protected
> - public
> - short
> - static
> - super
> - synchronized
> - throws
> - transient
> - volatile

第 5 版把在非严格模式下运行时的保留字缩减为下列这些：

> - class
> - const
> - enum
> - export
> - extends
> - import
> - super

在严格模式下，第 5 版还对以下保留字施加了限制：

> - implements
> - interface
> - let
> - package
> - private
> - protected
> - public
> - static
> - yield

除了上面列出的保留字和关键字，ECMA-262 第 5 版对 eval 和 arguments 还施加了限制。在严格模式下，这两个名字也不能作为标识符或者属性名，否则会抛出错误。

## 原型

每一个 JavaScript 对象（`null` 除外）都和另一个对象相关联。

## 继承

JS 是基于对象，没有类的概念。实现继承，用 JS 原型  `prototype` 机制或者用 `apply` 和 `call` 方法来实现。

JS对象具有“自有属性”，也有一些属性是从原型对象继承而来的。对象的原型属性构成了一个“链”，通过原型链可以实现属性的继承。

比如要查询对象 `obj` 的属性 `x` ，如果 `obj` 中不存在 `x` ，那么将会继承在 `obj` 中的原型对象中查找属性 `x` ，如果原型对象中也没有 `x` ，但这个原型对象也有原型，那么继续在这个原型对象的原型上执行查询，直到找到 `x` 或者找到一个原型是 `null` 的对象为止。

在 JS 中，只有在查询属性时才会体会到继承的存在，而设置属性则和继承无关。

## 闭包

闭包是指有权访问另一个函数作用域中的变量的函数，创建闭包的最常用的方式就是在一个函数内创建另一个函数，通过另一个函数访问这个函数的局部变量。

**特点**：函数嵌套函数；函数内部可以引用外部的参数和变量；参数和变量不会被垃圾回收机制回收。

**优点**：变量长期驻扎在内存中；避免全局变量的污染；私有成员的存在。

**缺点**：常驻内存，会增大内存使用量，使用不当会造成内存泄漏。

## JS单线程

JS运行在浏览器中，是单线程的，每个window一个JS线程。既然是单线程，在某个特定的时刻只有特定的代码能够被执行，并阻塞其它的代码。而浏览器是事件驱动，浏览器中很多行为是异步的，会创建事件并放入队列中。JavaScript引擎是单线程处理它的任务队列。当异步事件发生时，比如鼠标点击事件、定时器触发事件、XMLHttpRequest完成回调触发等，将它们放入执行队列，等待当前代码执行完成。

## 冒泡事件和捕获事件

冒泡事件：鼠标点击了一个按钮，同样的事件将会在这个元素的所有祖先元素中被触发。这个事件从元素开始一直冒泡到 DOM 树的最上层。

## 事件阶段

> * 捕获阶段：在事件对象到达事件目标之前，事件对象必须从 window 经过目标的祖先节点传播到事件目标。
> * 目标阶段：事件对象到达其事件目标。一旦事件对象到达事件目标，该阶段的事件监听器就要对它进行处理。
> * 冒泡阶段：从事件目标传播经过其祖先节点传播到 window。

## 事件代理

事件目标自身不处理事件，把处理任务委托给其父元素或者祖先元素，甚至根元素。因为绑定单击事件多导致脚本执行速度变慢，也占用大量内存。

优点：需要创建的以及驻留在内存中的事件处理器减少了；提高性能；降低浏览器崩溃的风险；无需绑定事件处理器。

## 原生ajax示例

```javascript
var request;
if(window.XMLHttpRequest) {
    request = new XMLHttpRequest();
}else {
    request = new ActiveXObject('Microsoft.XMLHTTP');// IE 5/6
}
request.onreadystatechange = function() {
    if(request.readyState == 4 && request.status == 200) {
        document.getElementById('div').innerHTML = request.responseText;
    }
};
request.open('GET', 'test.txt', true);
request.send();
```
