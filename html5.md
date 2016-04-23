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

可以使用下面的函数来检测：

```javascript
function supports_canvas() {
    return !!document.createElement('canvas').getContext;
}
```

检测浏览器是否支持 canvas API 还可以使用 Modernizr 库检测，具体代码查看上一知识点。

## 画布文本

浏览器支持 canvas API 并不意味着它也一定支持 canvas 文本 API，原因是 canvas API 一直在不断完善中，绘制文本的函数后来才被纳入规范。一些浏览器在文本 API 最终确定之前就引入了对 `canvas` 的支持。

可以使用下面的函数来检测：

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

可以使用下面的函数来检测：

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