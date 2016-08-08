Canvas 元素用于在网页上绘制图形。
--

**1、什么是 Canvas？**

　　HTML5 的 canvas 元素使用 JavaScript 在网页上绘制图像。画布是一个矩形区域，您可以控制其每一像素。canvas 拥有多种绘制路径、矩形、圆形、字符以及添加图像的方法。


**2.创建一个画布（Canvas）**
	
	//HTML
	<canvas  id="myCanvas" width="200" height="100" 
	style="border:1px solid #000000;">
	</canvas>

**3.通过 JavaScript 来绘制**

canvas 元素本身是没有绘图能力的。所有的绘制工作必须在 JavaScript 内部完成：

	//js
	<script type="text/javascript">
	var c=document.getElementById("myCanvas");
	var cxt=c.getContext("2d");
	cxt.fillStyle="#FF0000";
	cxt.fillRect(0,0,150,75);
	</script>

**4.Canvas-路径**

**直线：**

1. moveTo(x,y) 定义线条开始坐标
2. lineTo(x,y) 定义线条结束坐标

绘制线条我们必须使用到 "ink" 的方法，就像stroke()。

实例：

定义开始坐标(0,0), 和结束坐标 (200,100). 然后使用 stroke() 方法来绘制线条:

	//绘制线条
	<script type="text/javascript">
	var c=document.getElementById("myCanvas");
	var ctx=c.getContext("2d");
	ctx.moveTo(0,0);
	ctx.lineTo(200,100);
	ctx.stroke();
	</script>

**圆：**

arc(x,y,r,start,stop)

	//绘制圆
	var c=document.getElementById("myCanvas");
	var ctx=c.getContext("2d");
	ctx.beginPath();
	ctx.arc(95,50,40,0,2*Math.PI);
	ctx.stroke();

**曲线：**

quadraticCurveTo() 方法通过使用表示二次贝塞尔曲线的指定控制点，向当前路径添加一个点。

1. 开始点：moveTo(188,150)
2. 控制点：quadraticCurveTo(288, 0, 388, 150);
3. 结束点：quadraticCurveTo(288, 0, 388, 150)



		var canvas = document.getElementById('myCanvas');
		var context = canvas.getContext('2d');
		context.beginPath();
		context.moveTo(188, 150);
		context.quadraticCurveTo(288, 0, 388, 150);
		context.lineWidth = 10;
		// line color
		context.strokeStyle = 'orange';
		context.stroke();	


**渐变：**

渐变可以填充在矩形, 圆形, 线条, 文本等等, 各种形状可以自己定义不同的颜色。

两种不同的方式来设置Canvas渐变：

1. createLinearGradient(x,y,x1,y1) - 创建线条渐变
2. createRadialGradient(x,y,r,x1,y1,r1) - 创建一个径向/圆渐变


		var c=document.getElementById("myCanvas");
		var cxt=c.getContext("2d");
		var grd=cxt.createLinearGradient(0,0,175,50);
		grd.addColorStop(0,"#FF0000");
		grd.addColorStop(1,"#00FF00");
		cxt.fillStyle=grd;
		cxt.fillRect(0,0,175,50);

**图像：**

把一幅图像放置到画布上, 使用以下方法:

drawImage(image,x,y)

	   //图像
       var c=document.getElementById("myCanvas");
       var ctx=c.getContext("2d");
       var img=document.getElementById("scream");
       ctx.drawImage(img,10,10);