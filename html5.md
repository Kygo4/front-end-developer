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