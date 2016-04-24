# HTML5

## 检测技术

有四种基本技术可以用于检测浏览器是否支持某种 HTML5 特性：

> - 检测全局对象（诸如 `window` 或者 `navigator`）是否拥有特定的属性；
> - 创建一个元素，然后检查该元素的 DOM 对象是否拥有特定的属性；
> - 创建一个元素，然后检测这个元素的 DOM　对象是否拥有特定的方法，同时调用这个方法并检查它的返回值；
> - 创建一个元素，给这个元素的 DOM 对象设定特定的属性值，然后检查浏览器是否保留了该属性。

## Modernizr：一个 HTML5 特性检测库

Modernizr 是一个基于 MIT 许可证书发布的开源 JavaScript 类库，用于检测浏览器是否支持 HTML5 及 CSS3 特性。

```html
<script src="modernizr.min.js"></script>
```

Modernizr 是自动运行的，无需调用诸如 `modernizr_init()` 之类的初始化方法。当它运行的时候，会创建一个名为 Modernizr 的全局对象，这个对象为每一个可检测的特性创建了一个对应的布尔类型的属性。

例如，如果你的浏览器支持画布 API，那么 `Modernizr.canvas` 的属性值就为 `true`，反之，则为 `false`：

```javascript
if (Modernizr.canvas) {
    // code
} else {
    // code
}
```

## 画布

HTML5 中定义 `<canvas>` 元素为：“它是依赖分辨率的位图画布，你可以在 `canvas` 上面绘制任意图形，甚至加载图片。”。在网页中，一个 `canvas` 就是一个矩形区域。你可以在这个区域内通过 JavaScript 画你想画的任何东西。HTML5 标准中定义了一系列的 canvas API，用于绘制简单图形、定义路径、创建渐变及应用图像变换。

可以使用下面的函数来检测浏览器是否支持 canvas API：

```javascript
function supports_canvas() {
    return !!document.createElement('canvas').getContext;
}
```

检测浏览器是否支持 canvas API 还可以使用 Modernizr 库检测，具体代码查看上一知识点。

## 画布文本

浏览器支持 canvas API 并不意味着它也一定支持 canvas 文本 API，原因是 canvas API 一直在不断完善中，绘制文本的函数后来才被纳入规范。一些浏览器在文本 API 最终确定之前就引入了对 `canvas` 的支持。

可以使用下面的函数来检测浏览器是否支持 canvas 文本 API：

```javascript
function supports_canvas_text() {
    if (!supports_canvas()) {return false;}
    var dummy_canvas = document.createElement('canvas');
    var context = dummy_canvas.getContext('2d');
    return typeof context.fillText == 'function';
}
```

检测浏览器是否支持 canvas 文本 API 还可以使用 Modernizr 库检测：

```javascript
if (Modernizr.canvastext) {
    // code
} else {
    // code
}
```

## 视频

HTML5 标准中定义了一个新的元素：`<video>`，用来将视频内嵌到 Web 页面中。

`<video>` 元素的可用性有意设计为不需要任何脚本来检测。你可以指定多个视频文件，支持 HTML5 video 的浏览器会选择一个它支持的视频格式来进行播放。不支持 HTML5 video 的浏览器会完全忽略 `<video>` 元素，可以指定第三方插件来播放视频。

可以使用下面的函数来检测浏览器是否支持 HTML5 video：

```javascript
function supports_video() {
    return !!document.createElement('video').canPlayType;
}
```

检测浏览器是否支持 HTML5 video 还可以使用 Modernizr 库检测：

```javascript
if (Modernizr.video) {
    // code
} else {
    // code
}
```

## 视频格式

对于一个视频，浏览器要想播放它，必须要理解视频是用哪种编码算法（一种用来将视频编码成比特流的算法）。世界上有许许多多的视频算法，各种浏览器没有使用统一的视频编码算法。但好在分歧已缩减到两种算法上：

> - Safari 和 iPhone （如果你使用“视频无处不在”的解决方案的话还有 Adobe 的 Flash）遵循的需要收费的编码算法；
> - 诸如 Chromium 和 Mozilla Firefox 这类开源浏览器遵循的免费的编码算法。

检测 Mac 和 iPhone 支持的受专利保护的格式：

```javascript
function supports_h264_baseline_video() {
    if (!supports_video()) {return false;}
    var v = document.createElement('video');
    return v.canPlayType('video/mp4; codecs = "avc1.42E01E, mp4a.40.2"');
}
```

调用 `canPlayType()` 方法不会返回布尔值。因为视频格式非常复杂，所以这个方法返回一个字符串：

> - `"probably"`：表示浏览器有充分把握可以播放此格式；
> - `"maybe"`：表示浏览器有可能可以播放此格式；
> - `""`（空字符串）：表示浏览器确定无法此格式。

检测被 Mozilla Firefox 和其他一些开源浏览器支持的开发视频格式：

```javascript
function supports_ogg_theora_video() {
    if (!support_video()) {return false;}
    var v = document.createElement('video');
    return v.canPlayType('video/ogg; codecs = "theora, vorbis"');
}
```

WebM 是一种新的开源（不受专利约束）视频编码格式。检测浏览器是否支持 WebM 视频格式：

```javascript
function supports_webm_video() {
    if (!support_video()) {return false;}
    var v = document.createElement('video');
    return v.canPlayType('video/webm; codecs = "vp8, vorbis"');
}
```

检测浏览器是否支持上述提到的各种 HTML5 视频格式还可以使用 Modernizr 库检测：

```javascript
if (Modernizr.video) {
    if (Modernizr.video.ogg) {
        // code
    } else if (Modernizr.video.h264) {
        // code
    }
} else {
    // code
}
```

## 本地存储

HTML5 本地存储允许网站把信息存储到本地的计算机上，以便在以后需要时获取。这个概念和 cookie 相似，但它是为了更大容量的存储设计的。Cookie 的大小是受限的，并且每次请求一个新页面时，cookie 信息都会被发送回服务器（不仅耗费额外的时间，而且占用宝贵的带宽）。而 HTML5 本地存储将信息存储在用户本地计算机上，网站可以在页面加载完毕后通过 JavaScript 获取。

可以使用下面的函数来检测浏览器是否支持 HTML5 本地存储：

```javascript
function supports_local_storage() {
    return ('localStorage' in window) && window['localStorage'] != null;
}
```

检测浏览器是否支持 HTML5 本地存储还可以使用 Modernizr 库检测：

```javascript
if (Modernizr.localstorage) {
    // code
} else {
    // code
}
```

任何物理上能访问你计算机的人都可以查看（或修改）你 HTML5 的本地数据库。在浏览器中，任何网站都可以读取和修改它们自己存储的数据，但是不同站点的存储数据是不能相互访问的（“同源限制”）。

## Web Workers

Web Workers 提供了一种标准的方式让浏览器能够在后台运行 JavaScript。通过 Web Workers。你可以产生多个“线程”，并让它们同时运行。（就像计算机能够同一时间运行多个应用程序一样）。这些“后台线程”可以在页面响应用户的滚屏、点击或者输入操作的同时做些诸如复杂的数学运算、发送网络请求或者操作本地数据库的事情。

可以使用下面的函数来检测浏览器是否支持 Web Worker：

```javascript
function supports_web_workers() {
    return !!window.Worker;
}
```

检测浏览器是否支持 Web Worker 还可以使用 Modernizr 库检测：

```javascript
if (Modernizr.webworkers) {
    // code
} else {
    // code
}
```

## 离线 Web 应用

离线 Web 应用首先要从在线 web 应用开始。在第一次访问具备离线访问功能的 Web 站点时，Web 服务器会告诉浏览器哪些文件是保证离线正常工作所必需的，这些文件可以在任意文件 —— HTML、JavaScript、图片甚至视频。一旦浏览器下载了这些必需的文件之后，下次哪怕在没有网络的情况下也能正常访问该站点。浏览器会识别到当前是离线状态，并使用那些之前下载下来的文件。当你重新上线的时候，所有改动都会上传到远程 Web 服务器。

可以使用下面的函数来检测浏览器是否支持离线 Web 应用：

```javascript
function supports_offline() {
    return !!window.applicationCache;
}
```

检测浏览器否支持离线 Web 应用还可以使用 Modernizr 库检测：

```javascript
if (Modernizr.applicationcache) {
    // code
} else {
    // code
}
```

## 地理位置

地理位置能够神奇的定位出你正待在世界上的什么地方，并且在你允许的情况下把该位置信息分享给你信任的人。定位的方法有很多 —— IP 地址、利用基站获取手机无线网络的接入位置、通过能够利用卫星定位获取经纬度信息的 GPS 设备。

可以使用下面的函数来检测浏览器是否支持地理位置特性：

```javascript
function supports_geolocation() {
    return !!navigator.geolocation;
}
```

检测浏览器否支持地理位置特性还可以使用 Modernizr 库检测：

```javascript
if (Modernizr.geolocation) {
    // code
} else {
    // code
}
```

## 输入框类型

HTML5 标准中定义了很多的新输入框类型：

```html
<!--表示搜索框-->
<input type="search">
<!--表示数字类型输入框-->
<input type="number">
<!--表示范围选择滑块-->
<input type="range">
<!--表示颜色选择器-->
<input type="color">
<!--表示电话号码输入框-->
<input type="tel">
<!--表示网址输入框-->
<input type="url">
<!--表示 email 地址输入框-->
<input type="email">
<!--表示日期选择器->
<input type="date">
<!--表示月份输入框-->
<input type="month">
<!--表示星期输入框-->
<input type="week">
<!--表示时间戳输入框-->
<input type="time">
<!--表示精确日期 / 时间戳输入框-->
<input type="datetime">
<!--表示当地日期和时间输入框-->
<input type="datetime-local">
```

可以使用下面的函数来检测浏览器是否支持新的输入框类型：

首先，创建一个虚拟的 `<input>` 元素：

```javascript
var i = document.createElement('input');
```

将 `<input>` 元素的类型设置成你要检测的类型：

```javascript
i.setAttribute("type", "color");
```

如果浏览器支持此特定的输入框类型，那么设置的 `type` 属性值会被保留。反之，浏览器会忽略你设置的值，`type` 属性的值依然为 `"text"`：

```javascript
return i.type !== "text";
```

针对 13 种不同输入框类型的检测就意味着要写 13 个检测方法，如果不想自己去写这些方法的话，可以使用 Modernizr 库提供的方法检测浏览器是否支持这些新的输入框类型。Modernizr 库重用一个 `<input>` 元素来高效检测 13 种输入框类型，然后构造了一个名为 `Modernizr.inputtypes` 的散列表，这些散列表中包含 13 个键值对，其中，键表示类型（即 HTML5 新增的输入框类型属性名），值是布尔值（`true` 表示支持该类型，`false` 则表示不支持该类型）;

```javascript
if (!Modernizr.inputtypes.date) {
    // 浏览器没有提供 <input type="date"> 原生支持
    // 也许你需要自己用 Dojo 或 JqueryUI 来构造一个类似的控件
}
```

## 占位文本

除了新的输入框类型，HTML5 标准中还给现有的表单控件做了一些小改进，其中一个改进就是给输入框设置占位文本。占位文本会在输入框为空或者失去焦点的时候显示出来，一旦用户点击输入框（或者利用 Tab 键使其获得焦点），占位文本就会消失。

可以使用下面的函数来检测浏览器是否支持占位文本：

```javascript
function supports_input_placeholder() {
    var i = document.createElement('input');
    return 'placeholder' in i;
}
```

检测浏览器否支持占位文本还可以使用 Modernizr 库检测：

```javascript
if (Modernizr.input.placeholder) {
    // code
} else {
    // code
}
```

## 表单自动聚焦

HTML5 标准中为所有的表单控件引入了一个 `autofocus` 属性，将焦点自动聚焦到特定的输入框中。由于是直接采用标记而不是 JavaScript 实现这一功能，因此所有网站的行为保持一致。

可以使用下面的函数来检测浏览器是否支持自动聚焦：

```javascript
function supports_input_autofocus() {
    var i = document.createElement('input');
    return 'autofocus' in i;
}
```

检测浏览器否支持自动聚焦还可以使用 Modernizr 库检测：

```javascript
if (Modernizr.input.autofocus) {
    // code
} else {
    // code
}
```

## 微数据

微数据是一种标准化的为 Web 页面提供额外语义的方式。例如，可以使用微数据来声明一张图片是被特定的创作公用许可证授权使用的。浏览器、浏览器扩展程序及搜索引擎能把微数据的标记转换为 VCard 形式（一种用于共享联系人信息的标准格式）。也可以定义属于自己的微数据词汇。

HTML5 微数据标准包含 HTML 标记（主要用于搜索引擎）和一系列的 DOM 方法（主要用于浏览器）。在页面中使用微数据标记不会带来什么损害，因为顶多就是一些被适当放置的属性罢了，并且如果搜索引擎无法识别这些微数据属性，就会直接忽略掉。但是如果想要通过 DOM 访问和操作微数据，那就得确保浏览器支持微数据的 DOM API。

可以使用下面的函数来检测浏览器是否支持 HTML5 微数据 API：

```javascript
function supports_microdata_api() {
    return !!document.getItems;
}
```

Modernizr 目前还不支持检测微数据 API，所以必须用类似这样的一个函数来检测。