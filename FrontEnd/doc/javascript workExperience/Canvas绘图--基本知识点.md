Canvas绘图--基本知识点
--
> 本文参考http://www.cnblogs.com/picaso/archive/2012/11/26/2789077.html

**绘制普通线段：**


	 //绘制普通线段
    (function(){
        var canvas =document.getElementById("myCanvas")
        var ctx = canvas.getContext('2d');
             ctx.moveTo(0,0); //线段起点
             ctx.lineTo(100,100);//线段第二点
             ctx.lineTo(260,180);//线段第三点
             ctx.lineWidth = 3;
             ctx.strokeStyle='red';//绘制样式
             ctx.stroke();//绘制路径

    })();

**绘制颜色渐变线段：**

	 (function(){
	        var cans = document.getElementById("myCanvas"),
	             ctx = cans.getContext('2d');
	             ctx.moveTo(0,0);
	             ctx.lineTo(300,300);
	            var gnt = ctx.createLinearGradient(0,0,300,300);
	            gnt.addColorStop(0,'blue');
	            gnt.addColorStop(0.2,'green');
	            gnt.addColorStop(1,'#b2b2b2');
	            ctx.lineWidth=3;
	            ctx.strokeStyle = gnt;
	            ctx.stroke();
	
	    })();


