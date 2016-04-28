# JavaScript

## JavaScript实现

一个完整的 JavaScript 实现由核心（ECMAScript）、文档对象模型（DOM）、浏览器对象模型（BOM）三部分组成。

- **ECMAScript**：由 ECMA-262 定义的 ECMAScript 与 Web 浏览器没有依赖关系。ECMA-262 规定了这门语言的组成部分有语法、类型、语句、关键字、保留字、操作符和对象。ECMAScript 就是对实现该标准规定的各个方面内容的语言的描述；**（由 ECMA-262 定义，提供核心语言功能。）**
- **文档对象模型（DOM）**：文档对象模型（DOM，Document Object Model）是针对 XML 但经过扩展用于 HTML 的应用程序编程接口（API，Application Programming Interface）；**（提供访问和操作网页内容的方法和接口。）**
- **浏览器对象模型（BOM）**：浏览器对象模型（BOM，Browser Object Model）支持可以访问和操作浏览器窗口。开发人员使用 BOM 可以控制浏览器显示的页面以外的部分。**（提供与浏览器交互的方法和接口。）**

## `<script>`元素

把 JavaScript 插入到 HTML 页面中要使用 `<script>` 标签。使用这个元素可以把 JavaScript 嵌入到 HTML 页面中，让脚本与标记混合在一起；也可以包含外部的 JavaScript 文件。而我们需要注意的地方有：

- 在包含外部 JavaScript 文件时，必须将 `src` 属性设置为指向相应文件的 URL。而这个文件既可以是与包含它的页面位于同一个服务器上的文件，也可以是其他任何域中的文件；
- 所有 `<script>` 元素都会按照它们在页面中出现的先后顺序依次被解析。在不使用 `defer` 和 `async` 属性的情况下，只有在解析完前面 `<script>` 元素的代码之后，才会开始解析后面 `<script>` 元素中的代码；
- 由于浏览器会先解析完不使用 `defer` 属性的 `<script>` 元素中的代码，然后再解析后面的内容，所以一般应该把 `<script>` 元素放在页面最后，即主要内容后面，`</body>` 标签前面；
- 使用 `defer` 属性可以让脚本在文档完全呈现之后再执行。延迟脚本总是按照指定它们的顺序执行；
- 使用 `async` 属性可以表示当前脚本不必等待其他脚本，也不必阻塞文档呈现。不能保证异步脚本按照它们在页面中出现的顺序执行。

另外，使用 `<noscript>` 元素可以指定在不支持脚本的浏览器中显示的替代内容。但在启用了脚本的情况下，浏览器不会显示 `<noscript>` 元素中的任何内容。

## 标识符

所谓标识符，就是指变量、函数、属性的名字，或者函数的参数。标识符可以是按照下列格式规则组合起来的一或多个字符：
> - 第一个字符必须是一个字母、下划线（`_`）或一个美元符号（`$`）;
> - 其他字符可以是字母、下划线、美元符或数字。

标识符中的字母也可以包含扩展的 ASCII 或 Unicode 字母字符，但我们不推荐这样做。

按照惯例，ECMAScript 标识符采用 **驼峰大小写格式**，也就是第一个字母小写，剩下的每个单词的首字母大写。**（为了与 ECMAScript 内置的函数和对象命名格式保持一致）**

## 关键字和关键字

- 关键字

ECMA-262 描述了一组具有特定用途的关键字，这些关键字可用于表示控制语句的开始或结束，或者用于执行特定操作等。按照规则，关键字也是语言保留的，不能用作标识符。以下就是 ECMAScript 的全部关键字（带 `*` 号上标的是第 5 版新增的关键字）：

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

除了上面列出的保留字和关键字，ECMA-262 第 5 版对 `eval` 和 `arguments` 还施加了限制。在严格模式下，这两个名字也不能作为标识符或者属性名，否则会抛出错误。

## 数据类型

ECMAScript 中有 5 种简单数据类型（基本数据类型）：`Undefined`、`Null`、`Boolean`、`Number` 和 `String`。还有 1 种复杂数据结构 -- `Object`，`Object` 本质上是由一组无序的名值对组成的。

- `Undefined` 类型

`Undefined` 类型只有一个值，即特殊的 `undefined`。在使用 `var` 声明变量但未对其加以初始化时，这个变量的值就是 `undefined`。对于尚未声明过的变量，只能执行一项操作，即使用 `typeof` 操作符检测其数据类型（对未经声明的变量调用 `delete` 不会导致错误，但这样做没什么实际意义，而且在严格模式下确实会导致错误）。

- `Null` 类型

`Null` 类型只有一个值，即特殊的 `null`。从逻辑角度来看，`null` 值表示一个空对象指针，而这也正是使用 `typeof` 操作符检测 `null` 值时会返回 `"object"` 的原因。如果定义的变量准备在将来用于保存对象，那么最好将该变量初始化为 `null` 而不是其他值。实际上，`undefined` 值是派生自 `null` 值，因此  ECMA-262 规定对它们的相等性测试（`==`）返回 `true`。

- `Boolean` 类型

`Boolean` 类型是 ECMAScript 中使用得最多的一种类型，该类型只有两个值：`true` 和 `false`。`true` 不一定等于 `1`，`false` 也不一定等于 `0`。虽然 `Boolean` 类型的字面值只有两个，但 ECMAScript 中所有类型的值都有与这两个 `Boolean` 值等价的值。将一个值转换为其对应的 `Boolean` 值，可以调用转型函数 `Boolean()`。

|数据类型|转换为 true 的值|转换为 false 的值|
| -------- | :----: | :----: |
|`Boolean`|`true`|`false`|
|`String`|任何非空字符串|`""`（字符串）|
|`Number`|任何非零数字值（包括无穷大）|`0` 和 `NaN`|
|`Object`|任何对象|`null`|
|`Undefined`|不适用|`undefined`|

- `Number` 类型

`Number` 类型应该是 ECMAScript 中最令人关注的数据类型了，这种类型使用 IEEE754 格式来表示整数和浮点数值。

> - 浮点数值。所谓浮点数值，就是该数值中必须包含一个小数点，并且小数点后面必须至少有一位数字。由于保存浮点数值需要的内存空间是保存整数的两倍，因此 ECMAScript 会不失时机地将浮点数值转换为整数值。浮点数值的最高精度是 17 位小数，但在进行算术计算时其精确度远远不如整数。例如，`0.1` 加 `0.2` 的结果不是 `0.3`，而是 `0.30000000000000004`；
> - 数值范围。ECMAScript 能够表示的最小数值保存在 `Number.MIN_VALUE` 中，最大数值保存在 `Number.MAX_VALUE` 中。超出 JavaScript 数值范围的值被自动转换成特殊的 `Infinity` 值。正数转换成 `Infinity`（正无穷），负数转换成 `-Infinity`（负无穷）。确定一个数值是不是有穷的，可以使用 `isFinite()` 函数；
> - `NaN`。`NaN`，即非数值（Not a Number）是一个特殊的数值，用于表示要返回数值的操作数未返回数值的情况。任何涉及 `NaN` 的操作都返回 `NaN`，`NaN` 与任何值都不相等，包括 `NaN` 本身。`isNaN()` 函数接受一个任意类型的参数，确定这个参数是否“不是数值”；
> - 数值转换。`Number()`、`parseInt()` 和 `parseFloat()` 可以把非数值转换为数值。`Number()` 用于任何数据类型，而 `parseInt()` 和 `parseFloat()` 用于把字符串转换成数值。

**`Number()` 函数的转换规则：**

> - 如果是 `Boolean` 值，`true` 和 `false` 将分别被转换为 `1` 和 `0`；
> - 如果是数字值，只是简单的传入和返回；
> - 如果是 `null` 值，返回 `0`；
> - 如果是 `undefined`，返回 `NaN`；
> - 如果是字符串，遵循下列规则：

>> - 如果字符串中只包含数字（包括前面带正号或负号的情况），则将其转换为十进制数值，即 `"1"` 会变成 `1`，`"123"` 会变成 `123`，而 `011` 会变成 `11`（注意：前导的零被忽略了）；
>> - 如果字符串中包含有效的浮点格式，如 `"1.1"`，则将其转换为对应的浮点数值（同样，也会忽略前导零）；
>> - 如果字符串中包含有效的十六进制格式，例如 `"0xf"`，则将其转换为相同大小的十进制整数值；
>> - 如果字符串是空的（不包含任何字符），则将其转换为 `0`；
>> - 如果字符串中包含除上述格式之外的字符，则将其转换为 `NaN`。

> - 如果是对象，则调用对象的 `valueOf()` 方法，然后依照前面的规则转换返回的值。如果转换的结果是 `NaN`，则调用对象的 `toString()` 方法，然后再次依照前面的规则转换返回的字符串值。

由于 `Number()` 函数在转换字符串时比较复杂而且不够合理，因此在处理整数的时候更常用的是 `parseInt()` 函数。`parseInt()` 函数在转换字符串时，更多的是看其是否符合数值模式。它会忽略字符串前面的空格，直至找到第一个非空格字符。如果第一个字符不是数字字符或者负号，`parseInt()` 就会返回 `NaN`；也就是说，用 `parseInt()` 转换空字符串会返回 `NaN`（`Number()` 对空字符返回 `0`）。如果第一个字符是数字字符，`parseInt()` 会继续解析第二个字符，直到解析完所有后续字符或者遇到了一个非数字字符。在 ECMAScript 5 JavaScript 引擎中，`parseInt()` 已经不具有解析八进制值得能力。为了消除这个问题，为这个函数提供了第二个参数：转换时使用的基数（即多少进制）。

与 `parseInt()` 函数类似，`parseFloat()` 也是从第一个字符（位置 0）开始解析每个字符。而且也是一直解析到字符串末尾，或者解析到遇见一个无效的浮点数字字符为止。除了第一个小数点有效之外，`parseFloat()` 与 `parseInt()` 的第二个区别在于它始终都会忽略前导的零。`parseFloat()` 只解析十进制值，因此它没有用第二个参数指定某数的用法。如果字符串包含的是一个可解析为整数的数（没有小数点，或者小数点后都是零），`parseFloat()` 会返回整数。

- String 类型

String 类型用于表示由零或多个 16 位 Unicode 字符组成的字符序列，即字符串。字符串可以由双引号（`"`）或单引号（`'`）表示。字符串一旦创建，它们的值就不能改变。要改变某个变量保存的字符串，首先要销毁原来的字符串，然后再用另一个包含新值得字符串填充该变量。

要把一个值转换为一个字符串有两种方式：

> - `toString()` 方法。数值、布尔值、对象和字符串值都有 `toString()` 方法（`null` 和 `undefined` 值没有这个方法）。多数情况下，调用 `toString()` 方法不必传递参数（例如： `100.toString();`）。但是，在调用数值的 `toString()` 方法时，可以传递一个参数：输出数值的基数（二进制、八进制、十进制（默认）、十六进制，乃至其他任意有效进制格式表示的字符串值。例如：`100.toString(16);`）；
> - 转型函数 `String()`。在不知道要转换的值是不是 `null` 或 `undefined` 的情况下。`String()` 函数遵循转换规则：

>> - 如果值有 `toString()` 方法，则调用该方法（没有参数）并返回相应的结果；
>> - 如果值是 `null`，则返回 `"null"`；
>> - 如果值是 `undefined`，则返回 `"undefined"`。

- `Object` 类型

ECMAScript 中的对象其实就是一组数据和功能的集合。对象可以通过执行  `new` 操作符后跟要创建的对象类型的名称来创建。`Object` 的每个实例具有下列属性和方法：

> - `constructor`：保存着用于创建当前对象的函数。对于 `var o = new Object();` 而言，构造函数就是 `Object()`；
> - `hasOwnProperty(propertyName)`：用于检查给定的属性在当前对象实例中（而不是在实例的原型中）是否存在。其中，作为参数的属性名（`propertyName`）必须以字符串形式指定（例如：`o.hasOwnProperty("name")`）；
> - `isPrototypeOf(object)`：用于检查传入的对象是否是传入对象的原型；
> - `propertyIsEnumerable(propertyName)`：用于检查给定的属性是否能够使用 `for-in` 语句来枚举。与 `hasOwnProperty()` 方法一样，作为参数的属性名必须与字符串形式指定；
> - `toLocaleString()`：返回对象的字符串表示，该字符串与执行环境的地区对应；
> - `toString()`：返回对象的字符串表示；
> - `valueOf()`：返回对象的字符串、数值或布尔值表示。通常与 `toString()` 方法的返回值相同。

## 垃圾收集

JavaScript 具有自动垃圾收集机制，也就是说，执行环境会负责管理代码执行过程中使用的内存。

- 标记清除

JavaScript 中最常用的垃圾收集方式是标记清除（mark-and-sweep）。当变量进入环境（例如，在函数中声明一个变量）时，就将这个变量标记为“进入环境”。从逻辑上讲，永远不能释放进入环境的变量所占用的内存，因为只要执行流进入相应的环境，就可能会用到它们。而当变量离开环境时，则将其标记为“离开环境”。

垃圾收集器在运行的时候会给存储在内存中的所有变量都加上标记（当然，可以使用任何标记方式。）然后，它会去掉环境中的变量以及被环境中的变量引用的变量的标记。而在此之后再被加上标记的变量将被视为准备删除的变量，原因是环境中的变量已经无法访问到这些变量了。最后，垃圾收集器完成内存清除工作，销毁那些带标记的值并回收它们所占用的内存空间。

- 引用计数

JavaScript 中不太常见的垃圾收集方式是引用计数（reference-counting）。跟踪记录每个值被引用的次数。当声明了一个变量并将一个引用类型值赋给该变量时，则这个值得引用次数就是 1。如果同一个值又被赋给另一个变量，则该值的引用次数加 1。相反，如果包含对这个值引用的变量又取得了另外一个值，则这个值得引用次数减 1。当这个值的引用次数变成 0 时，则说明没有办法再访问这个值了，因而就可以将其占用的内存空间回收回来。这样，当垃圾收集器下次再运行时，它就会释放那些引用次数为零的值所占用的内存。

IE 中有一部分对象并不是原生 JavaScript 对象。例如，其 BOM 和 DOM 中的对象就是使用 C++ 以 COM（Component　Object　Model，组件对象模型）对象的形式存在的，而　COM 对象的垃圾收集机制采用的就是引用计数策略。因此，即使 IE 的 JavaScript 引擎是使用标记清除策略来实现的，但 JavaScript 访问的 COM 对象依然是基于引用计数策略的。换句话说，只要在 IE 中涉及 COM 对象，就会存在 **循环引用** 的问题。IE9 把 BOM 和 DOM 对象都转换成了真正的 JavaScript 对象。这样，就避免了两种垃圾收集算法并存导致的问题，也消除了常见的内存泄漏现象。

## 引用类型

引用类型的值（对象）是 **引用类型** 的一个实例。在 ECMAScript 中，引用类型是一种数据结构，用于将数据和功能组织在一起。

- `Object` 类型

大多数引用类型值都是 `Object` 类型的实例；而且，`Object` 也是 ECMAScript 中使用最多的一个类型。

创建 `Object` 实例的方式有两种。第一种是使用 `new` 操作符后跟 `Object` 构造函数：

```javascript
var person = new Object();
person.name = "JavasCript";
person.age = 24;
```

另一种方式是使用对象字面量表示法：
```javascript
var person = {
    name: "JavasCript",
    age: 24
};
```

- `Array` 类型

除了 `Object` 之外，`Array` 类型恐怕是 ECMAScript 中最常用的类型。ECMAScript 数组的每一项可以保存任何类型的数据，数据的大小可以动态调整。

创建数组的基本方式有两种。第一种是使用 `Array` 构造函数：
```javascript
var colors = new Array();
// 预先知道数组要保存的项目数量
var colors = new Array(20);
// 传递数组中包含的项
var colors = new Array("red", "blue", "green");
```

另一种基本方式是使用数组字面量表示法：
```javascript
// 创建一个空数组
var names = [];
// 创建一个包含 3 个字符串的数组
var colors = ["red", "blue", "green"];
```

> - 检测数组

>> - 对于一个网页或者一个全局作用域而言，使用 `instanceof` 操作符；`if(value instanceof Array) {// 对数组执行某些操作}`
>> - ECMAScript5 新增 `Array.isArray()` 方法，确定某个值是不是数组，不管它是在哪个全局环境中创建。`if(Array.isArray(value)) {// 对数组执行某些操作}`

> - 转换方法

>> - `toLocaleString()` 方法；
>> - `toString()` 方法；
>> - `valueOf()` 方法。

> - 栈方法

>> - `push()` 方法，接收任意数量的参数，逐个添加到数组末尾，并返回修改后数组的长度；
>> - `pop()` 方法，从数组末尾移除最后一项，减少数组的 `length` 值，然后返回移除的值。

> - 队列方法

>> - `unshift()` 方法，在数组前端添加任意个项并返回新数组的长度；
>> - `shift()` 方法，移除数组中的第一项并返回该项，同时将数组长度减 1。

> - 重排序方法

>> - reverse() 方法，反转数组项的顺序；
>> - sort() 方法，按升序排列数组项。

> - 操作方法

>> - `concat()` 方法，在没有给 `concat()`  方法传递参数的情况下，它只是复制当前数组并返回副本。如果传递给 `concat()` 方法的是一或多个数组，则该方法会将这些数组中每一项都添加到结果中。如果传递的值不是数组，这些值就会简单地添加到结果数组的末尾。`concat()` 不会修改调用的数组；
>> - `slice()` 方法，返回的数组包含第一个参数指定的位置和所有到但不包含第二个参数指定的位置之间的所有数组元素。如果有一个参数，`slice()` 方法返回从该参数指定位置开始到当前数组末尾的所有项。如果有两个参数，`slice()` 方法返回起始和结束位置之间的项（不包含结束位置的项）。`slice()` 不会修改调用的数组；
>> - `splice()` 方法，在数组中插入或删除元素的通用方法。①**删除**：可以删除任意数量的项，只需指定 2 个参数：要删除的第一项的位置和要删除的项数。`splice(0, 2)` 会删除数组中的前两项。②**插入**：可以向指定位置插入任意数量的项，只需提供 3 个参数：起始位置、0（要删除的项数）和要插入的项。如果要插入多个项，可以再传入第四、第五，以至任意多个项。`splice(2, 0, "red", "green")` 会从当前数组的位置 2 开始插入字符串 `"red"` 和 `"green"`。③**替换**：可以向指定位置插入任意数量的项，且同时删除任意数量的项，只需指定 3 个参数：起始位置、要删除的项数和要插入的任意数量的项。插入的项数不必与删除的项数相等。`splice(2, 1, "red", "green")` 会删除当前数组位置 2 的项，然后再从位置 2 开始插入字符串 `"red"` 和 `"green"`。`splice()` 会修改调用的数组。

> - 位置方法。`indexOf()` 方法和 `lastIndexOf()` 方法都接收两个参数：要查找的项和（可选的）表示查找起点位置的索引。

>> - `indexOf()` 方法，从数组的开头（位置 0）开始向后查找；
>> - `lastIndexOf()` 方法，从数组的末尾开始向前查找。

> - 迭代方法。ECMAScript5 为数组定义了 5 个迭代方法。每个方法都接收两个参数：要在每一项上运行的函数和（可选的）运行该函数的作用域对象 -- 影响 `this` 的值。传入这些方法中的函数会接收三个参数：**数组项的值**、**该项在数组中的位置**和**数组对象本身**。

>> - `every()` 方法：对数组中的每一项运行给定函数，如果该函数对每一项都返回 `true`，则返回 `true`；
>> - `filter()` 方法：对数组中的每一项运行给定函数，返回该函数会返回 `true` 的项组成的数组；
>> - `forEach()` 方法：对数组中的每一项运行给定函数。这个方法没有返回值；
>> - `map()` 方法：对数组中的每一项运行给定函数，返回每次函数调用的结果组成的数组；
>> - `some()` 方法：对数组中的每一项运行给定函数，如果该函数对任一项返回 `true`，则返回 `true`。

> - 归并方法。ECMAScript5 还新增了两个归并数组的方法：`reduce()` 和 `reduceRight()`。这两个方法都会迭代数组的所有项，然后构建一个最终返回的值。这两个方法都接收两个参数：一个在每一项上调用的函数和（可选的）作为归并基础的初始值。传给 `reduce()` 和 `reduceRight()` 的函数接收 4 个参数： **前一个值**、**当前值**、**项的索引**和**数组对象**。这个函数返回的任何值都会作为第一个参数自动传给下一项。第一次迭代发生在数组的第二项上，因此第一个参数是数组的第一项，第二个参数就是数组的第二项。

>> - `reduce()` 方法，从数组的第一项开始，逐个遍历到最后；
>> - `reduceRight()` 方法，从数组的最后一项开始，向前遍历到第一项。

- `Date` 类型

ECMAScript 中的 `Date` 类型是在早期 Java 中的 `java.util.Date` 类基础上构建的。为此，`Date` 类型使用自 UTC（Coordinated Universal Time，国际协调时间）1970 年 1 月 1 日午夜（零时）开始经过的毫秒数来保存日期。在使用这种数据存储格式的条件下，`Date` 类型保存的日期能够精确到 1970 年 1 月 1 日之前或之后的 285616 年。

要创建一个日期对象，使用 `new` 操作符和 `Date` 构造函数即可。

```javascript
var now = new Date();
```

- `RegExp` 类型

ECMAScript 通过 `RegExp` 类型来支持正则表达式。使用下面类似 Perl 的语法，就可以创建一个正则表达式。

```javascript
var expression = / pattern / flags;
```

其中的模式（`pattern`）部分可以是任何简单或复杂的正则表达式，可以包含字符类、限定符、分组、向前查找以及反向引用。每个正则表达式都可带有一或多个标志（`flags`），用以标明正则表达式的行为。正则表达式的匹配模式支持下列 3 个标志。

> - `g`：表示全局（global）模式，即模式将被应用于所有字符串，而非在发现第一个匹配项时立即停止；
> - `i`：表示不区分大小写（case-insensitive）模式，即在确认匹配项时忽略模式与字符串的大小写；
> - `m`：表示多行（multiline）模式，即在到达一行文本末尾时还会继续查找下一行中是否存在与模式匹配的项。

创建正则表达式有两种方式。第一种是以字面量形式：

```javascript
// 匹配第一个 "bat" 或 "cat"，不区分大小写
var pattern1 = /[bc]at/i;
```

另一种是使用 `RegExp` 构造函数：

```javascript
// 与 pattern1 相同，只不过是使用构造函数创建的
var pattern2 = new RegExp("[bc]at", "i");
```

- `Function` 类型

每个函数都是 `Function` 类型的实例，而且都与其他引用类型一样具有属性和方法。由于函数是对象，因此函数名实际上也是一个指向函数对象的指针，不会与某个函数绑定。ECMAScript 中没有函数重载的概念。函数通常是使用函数声明语法定义的：

```javascript
function sum (num1, num2) {
    return num1 + num2;
}
```

还可以使用函数表达式定义函数：

```javascript
var sum = function(num1, num2) {
    return num1 + num2;
}
```

- 基本包装类型

为了便于操作基本类型值，ECMAScript 还提供了 3 个特殊的引用类型：`Boolean`、`Number` 和 `String`。**引用类型与基本包装类型的主要区别是对象的生存期。**

> - `Boolean` 类型。布尔表达式中的所有对象都会被转换为 `true`。`Boolean` 类型重写了 `valueOf()`、`toLocaleString()` 和 `toString()` 方法。基本类型与引用类型的布尔值还有两个区别。首先，`typeof` 操作符对基本类型返回 `boolean`，而对引用类型返回 `object`。其次，由于 `Boolean` 对象是 `Boolean` 类型的实例，所以使用 `instanceof` 操作符测试 `Boolean` 对象会返回 `true`，而测试基本类型的布尔值返回 `false`；

> - `Number` 类型。与 `Boolean` 类型一样，`Number` 类型也重写了 `valueOf()`、`toLocaleString()` 和 `toString()` 方法。重写后的 `valueOf()` 方法返回对象表示的基本类型的数值，另外两个方法则返回字符串形式的数值；

>> - `toFixed()` 方法，按照指定的小数位返回数值的字符串表示；
>> - `toExponential()` 方法，返回以指数表示法（也称 `e` 表示法）表示的数值的字符串形式；
>> - `toPrecision()` 方法，返回固定大小（fixed）格式，也可能返回指数（exponential）格式。根据要处理的数值决定到底是调用 `toFixed()` 还是调用 `toExponential()`。

> - `String` 类型。继承的 `valueOf()`、`toLocaleString()` 和 `toString()` 方法，都返回对象所表示的基本字符串值。

>> - 字符方法：`charAt()` 和 `charCodeAt()`；
>> - 字符串操作方法：`concat()`、`slice()`、`substr()` 和 `substring()`；
>> - 字符串位置方法：`index()` 和 `lastIndexOf()`；
>> - `trim()` 方法：创建一个字符串的副本，删除前置及后缀的所有空格，然后返回结果；
>> - 字符串大小写转换方法：`toLowerCase()`、`toLocaleLowerCase()`、`toUpperCase()` 和 `toLocaleUpperCase()`；
>> - 字符串模式匹配方法：`match()`、`search()`、`replace()` 和 `split()`；
>> - `localeCompare()` 方法：比较两个字符串，如果字符串在字母表中应该排在字符串参数之前，则返回一个负数（大多数情况下是 `-1`，具体的值要视实现而定）；如果字符串等于字符串参数，则返回 `0`；如果字符串在字母表中应该排在字符串参数之后，则返回一个正数（大多数情况下是 `1`，具体的值同样要视实现而定）；
>> - `fromCharCode()` 方法：接收一或多个字符编码，然后将它们转换成一个字符串。从本质上来看，这个方法与实例方法 `charCodeAt()` 执行的是相反的操作。

- 单体内置对象

由 ECMAScript 实现提供的、不依赖与宿主环境的对象，这些对象在 ECMAScript 程序执行之前就已经存在了。前面介绍了大多数的内置对象。例如 `Object`、`Array` 和 `String`。ECMA-262 还定义了两个单体内置对象：`Global` 和 `Math`。

> - `Global` 对象

>> - URI 编码方法：`encodeURI()`、`encodeURIComponent()`、`decodeURI()` 和 `decodeURIComponent()`；
>> - `eval()` 方法：解析代码字符串；
>> - `Global` 对象的属性：

>>> - `undefined`，特殊值 `undefined`
>>> - `NaN`，特殊值 `NaN`
>>> - `Infinity`，特殊值 `Infinity`
>>> - `Object`，构造函数 `Object`
>>> - `Array`，构造函数 `Array`
>>> - `Function`，构造函数 `Function`
>>> - `Boolean`，构造函数 `Boolean`
>>> - `String`，构造函数 `String`
>>> - `Number`，构造函数 `Number`
>>> - `Date`，构造函数 `Date`
>>> - `RegExp`，构造函数 `RegExp`
>>> - `Error`，构造函数 `Error`
>>> - `EvalError`，构造函数 `EvalError`
>>> - `RangeError`，构造函数 `RangeError`
>>> - `ReferenceError`，构造函数 `ReferenceError`
>>> - `SyntaxError`，构造函数 `SyntaxError`
>>> - `TypeError`，构造函数 `TypeError`
>>> - `URIError`，构造函数 `URIError`

>> - `window` 对象。

> - `Math` 对象

>> - `Math` 对象的属性：`Math.E` （自然对数的底数，即常量 `e` 的值）、`Math.LN10` （`10` 的自然对数）、`Math.LN2` （`2` 的自然对数）、`Math.LOG2E` （以 `2` 为底 `e` 的对数）、`Math.LOG10E` （以 `10` 为底 `e` 的对数）、`Math.PI` （`π` 的值）、`Math.SQRT1_2` （`1 / 2` 的平方根，即 `2` 的平方根的倒数）、`Math.SQRT2` （`2` 的平方根）；
>> - `min()` 和 `max()` 方法：用于确定一组数值中的最小值和最大值；
>> - 舍入方法：`Math.ceil()` 执行向上舍入，即它总是将数值向上舍入为最接近的整数，`Math.floor()` 执行向下舍入，即它总是将数值向下舍入为最接近的整数，`Math.round()` 执行标准舍入，即它总是将数值四舍五入为最接近的整数；
>> - `random()` 方法：返回大于等于 `0` 小于 `1` 的一个随机数；
>> - 其他方法：

>>> - `Math.abs(num)`，返回 `num` 的绝对值
>>> - `Math.exp(num)`，返回 `Math.E` 的 `num` 次幂
>>> - `Math.log(num)`，返回 `num` 的自然对数
>>> - `Math.pow(num)`，返回 `num` 的 `power` 次幂
>>> - `Math.sqrt(num)`，返回 `num` 的平方根
>>> - `Math.acos(x)`，返回 `x` 的反余弦值
>>> - `Math.asin(x)`，返回 `x` 的反正弦值
>>> - `Math.atan(x)`，返回 `x` 的反正切值
>>> - `Math.atan2(y, x)`，返回 `y / x` 的反正切值
>>> - `Math.cos(num)`，返回 `x` 的余弦值
>>> - `Math.sin(num)`，返回 `x` 的正弦值
>>> - `Math.tan(num)`，返回 `x` 的正切值


## 原型

每一个 JavaScript 对象（`null` 除外）都和另一个对象相关联。“另一个”对象就是我们熟悉的原型，每一个对象都从原型继承属性。

所有通过对象直接量创建的对象都具有同一个原型对象，并可以通过 JavaScript 代码 `Object.prototype` 获得对原型对象的引用。通过关键字 `new` 和构造函数调用创建的对象的原型就是构造函数的 `prototype` 属性的值。因此，同使用 `{}` 创建对象一样，通过 `new Object()` 创建的对象也继承自 `Object.prototype`。同样，通过 `new Array()` 创建的对象的原型就是 `Array.prototype`，通过 `new Date()` 创建的对象的原型就是 `Date.prototype`。

没有原型的对象为数不多，`Object.prototype` 就是其中之一。它不继承任何属性。其他原型对象都是普通对象，普通对象都具有原型。所有的内置构造函数（以及大部分自定义的构造函数）都具有一个继承自 `Object.prototype` 的原型。例如，`Date.prototype` 的属性继承自 `Object.prototype`，因此由 `new Date()` 创建的 `Date` 对象的属性同时继承自 `Date.prototype` 和 `Object.prototype`。这一系列链接的原型对象就是所谓的“原型链”（prototype chain）。

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

## 事件监听

## 冒泡事件和捕获事件

冒泡事件：鼠标点击了一个按钮，同样的事件将会在这个元素的所有祖先元素中被触发。这个事件从元素开始一直冒泡到 DOM 树的最上层。

## 事件阶段

> * 捕获阶段：在事件对象到达事件目标之前，事件对象必须从 `window` 经过目标的祖先节点传播到事件目标。
> * 目标阶段：事件对象到达其事件目标。一旦事件对象到达事件目标，该阶段的事件监听器就要对它进行处理。
> * 冒泡阶段：从事件目标传播经过其祖先节点传播到 `window`。

## 事件代理

事件目标自身不处理事件，把处理任务委托给其父元素或者祖先元素，甚至根元素。因为绑定单击事件多导致脚本执行速度变慢，也占用大量内存。

优点：需要创建的以及驻留在内存中的事件处理器减少了；提高性能；降低浏览器崩溃的风险；无需绑定事件处理器。

## 跨域

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

## setTimeout和setInterval区别

## 阻止元素默认行为

## 阻止冒泡事件
