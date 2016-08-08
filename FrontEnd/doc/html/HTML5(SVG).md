SVG学习
--
> http://www.w3school.com.cn/svg/index.asp

**1、什么是SVG？**

SVG 指可伸缩矢量图形 (Scalable Vector Graphics)

SVG 用于定义用于网络的基于矢量的图形

SVG 使用 XML 格式定义图形

SVG 图像在放大或改变尺寸的情况下其图形质量不会有损失

SVG 是万维网联盟的标准

**2、SVG优势**

SVG 图像可通过文本编辑器来创建和修改

SVG 图像可被搜索、索引、脚本化或压缩

SVG 是可伸缩的

SVG 图像可在任何的分辨率下被高质量地打印

SVG 可在图像质量不下降的情况下被放大


**3、HTML直接嵌入SVG**


	<!DOCTYPE html>
	<html lang="en">
	<head>
	    <meta charset="UTF-8">
	    <title>SVG's Demo</title>
	</head>
	<body>
	<div>
		//html直接嵌入SVG
	    <svg width="100%" height="100%" version="1.1" xmlns="http://www.w3.org/2000/svg">
	        <line xmlns="http://www.w3.org/2000/svg" x1="0" y1="0" x2="300" y2="300" style="stroke:rgb(99,99,99);stroke-width:2"/>
	    </svg>
	</div>
	</body>
	</html>

**4、HTML引入外部svg**


**SVG文件：**

	<?xml version="1.0" standalone="no"?>
	
	<!DOCTYPE svg PUBLIC "-//W3C//DTD SVG 1.1//EN"
	"http://www.w3.org/Graphics/SVG/1.1/DTD/svg11.dtd">
	
	<svg width="100%" height="100%" version="1.1"
	xmlns="http://www.w3.org/2000/svg">
	
	<circle cx="100" cy="50" r="40" stroke="black"
	stroke-width="2" fill="red"/>
	
	</svg>

**HTML文件：**


	<!DOCTYPE html>
	<html lang="en">
	<head>
	    <meta charset="UTF-8">
	    <title>SVG's Demo</title>
	</head>
	<body>
	<div>
	    <embed src="../img/svg/demo.svg" width="300" height="100"
	           type="image/svg+xml"
	           pluginspage="http://www.adobe.com/svg/viewer/install/" >
	    </embed>
	</div>
	</body>
	</html>

**Canvas 与 SVG 的比较：**


**Canvas：**


依赖分辨率

不支持事件处理器

弱的文本渲染能力

能够以 .png 或 .jpg 格式保存结果图像

最适合图像密集型的游戏，其中的许多对象会被频繁重绘


**SVG：**


不依赖分辨率

支持事件处理器

最适合带有大型渲染区域的应用程序（比如谷歌地图）

复杂度高会减慢渲染速度（任何过度使用 DOM 的应用都不快）

不适合游戏应用



**5、SVG各种实现
API http://www.w3school.com.cn/svg/svg_rect.asp**
