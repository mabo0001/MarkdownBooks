### 1.9　HTML5 Canvas对象

> 也可以使用CSS样式来改变画布的缩放比例。与调整大小不同，缩放提取当前画布的位图区域，然后重新取样以适应CCS样式中设定的宽度和高度的值。例如，将画布缩放到400 × 400区域，可以使用以下CSS样式。
> 第3章有一个使用变换矩阵缩放Canvas的示例。

Canvas对象是通过在HTML页面的<body>部分中放置<canvas>标签创建的，也可以通过以下代码创建画布实例。

```javascript
style="width: 400px; height:400px"
```

```javascript
var theCanvas = document.createElement("canvas");
```

Canvas对象有两个相关的属性和方法可以通过JavaScript访问：width和height。这些属性显示当前HTML页面创建的画布的宽度和高度。这里需要强调的是，这两个属性并不是只读的。例如，通过代码可以对它们进行更新，从而影响HTML页面上的对象。这意味着什么？这意味着用户可以在HTML页面上动态地调整画布尺寸而无须重新加载。

提示

Canvas对象目前有两个公共方法。第一个是getContext()，本章前面就使用过。本书将继续使用这个方法获得Canvas 2D环境对象的引用，这样才能在画布上进行绘图。第二个方法是toDataURL()，这个方法返回的数据是代表当前Canvas对象产生位图的字符串。它就像是屏幕的一个快照，通过提供一个不同的MIME类型作为参数，可以返回不同的数据格式。基本的格式是image/png，但是也可以获取image/jpeg和其他格式。下一个应用程序将会使用toDataURL()方法，把画布中的图像导出到另一个浏览器窗口。

提示

> 第三个公共的方法——toBlob()，已经被定义，并且正在不同的浏览器上实现该方法。toBlob（[callback]）将返回一个引用图像的文件，而不是一个base64编码的字符串。目前，尚未有任何浏览器实现该方法。

