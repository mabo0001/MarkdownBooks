### 20.1.1　GDI+概述

GDI(Windows Graphical Device Interface)技术是Windows操作系统提供的用来屏蔽绘图中硬件的差别，使应用程序在打印机上输出的和屏幕上输出的操作一样，只需告诉系统输出的设备是什么，采用相同的方法可以实现在不同的设备上进行输出。

GDI+是对GDI接口的进一步封装，它提供了比使用GDI进行图形图像处理更高效的方法，.Net框架提供了非常强大的GDI+类库，我们通过几个常用的类就可以完成日常的图形图像处理工作。GDI+主要提供了以下三方面的应用。

（1）矢量图形。矢量图具有颜色、形状、轮廓、大小和屏幕位置等属性。GDI+提供了存储图形这些基本信息的类、存储图形基元绘制方式信息的类以及实际进行绘制的类。

（2）图像处理。它主要指点阵图像或绘制图像，是由称做像素的单个点组成的，这些点可以进行不同的排列和染色以构成图样。图像往往无法使用二维矢量图形方式进行保存和处理。因此，GDI+提供了Bitmap、Image等类,它们可用于显示、操作和保存BMP、JPG、GIF等图像格式。矢量图形与图像最大的区别是矢量图不受分辨率的影响，因此在放大或缩小图形时不会影响出图的清晰度，而放大图像后，图像会变得模糊。

（3）文字显示。GDI+支持使用各种字体、字号和样式来显示文本。

我们在绘制图形图像的时候，需要定位它们的位置，GDI+的坐标系统默认原点(0,0)位于绘图表面的左上角，x轴正方向水平向右，y轴正方向垂直向下。

在绘图时，常用3种结构指定坐标：Point、Size和Rectangle。

（1）Point。GDI+使用Point表示一个点。这是一个二维平面上的点，即一个像素的表示方式。许多GDI+函数（如DrawLine()）以Point作为其参数。

（2）Size。GDI+使用Size表示一个尺寸（像素）。Size结构包含宽度和高度。它往往用来表示图形和图像的大小。

（3）Rectangle。原来表示一个指定的长形区域，它由一个Point和一个Size组成，其中Point表示矩形的左上角坐标位置，Size表示矩形的大小。

