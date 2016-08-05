html5/css3响应式布局介绍及设计流程
--
> http://www.51xuediannao.com/html+css/htmlcssjq/694.html


**html5/css3响应式布局开发流程**



第一步：Meta标签

	//IE8以上
	<meta name="viewport" content="width=device-width, initial-scale=1.0"> 


//IE8或更早不支持媒介查询

IE8或者更早的浏览器并不支持Media Query。你可以使用media-queries.js或者respond.js来为IE添加Media Query支持。 


	<!--[if lt IE 9]>    
	    <script src="http://css3-mediaqueries-js.googlecode.com/svn/trunk/css3-mediaqueries.js"></script>    
	<![endif]--> 


第二步：HTML结构

	//HTML
	<!DOCTYPE html>
	<html lang="en">
	<head>
	    <meta charset="UTF-8">
	    <title>Title</title>
	    <meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1, user-scalable=no">
	    <link href="../css/responsive.css" rel="stylesheet">
	</head>
	<body>
	    <div class="container">
	        <div class="header">Header</div>
	        <div class="content">
	            <div class="left">left</div>
	            <div class="right">right</div>
	        </div>
	        <div class="footer">Foot</div>
	    </div>
	</body>
	</html>

	//CSS
	

	body,div,dl,dt,dd,ul,ol,li,h1,h2,h3,h4,h5,h6,pre,form,fieldset,input,textarea,p,blockquote,th,td{margin:0;padding:0;}
	body{background:#fff;}
	table{border-collapse:collapse;border-spacing:0;}
	fieldset,img{border:0 none;}
	address,caption,cite,code,dfn,em,strong,th,var{font-style:normal;font-weight:normal;}
	strong{font-weight:800;}
	ol,ul,li{list-style:none outside none;}
	caption,th{text-align:left;}
	h1,h2,h3,h4,h5,h6{font-size:100%;font-weight:normal;}
	html{
	  height: 100%;
	}
	body{
	  height: 100%;
	}
	.container{
	  width: 100%;
	  height: 100%;
	}
	.header{
	  width: 100%;
	  height: 15%;
	  background-color: #bbbbbb;
	}
	.footer{
	  width: 100%;
	  background-color: red;
	  height: 10%;
	}
	
	@media screen and (max-width : 620px){
	  .content{
	    width: 100%;
	    height: 75%;
	    background-color: #00aaee;
	    & .left{
	      width: 100%;
	      float: left;
	      background-color: #b4b472;
	      height: 100%;
	    }
	    & .right{
	      width: 0;
	      float: left;
	      background-color: springgreen;
	      height: 100%;
	    }
	  }
	}
	@media screen and (min-width: 620px) and (max-width: 1960px){
	  .content{
	    width: 100%;
	    height: 75%;
	    background-color: #00aaee;
	    & .left{
	      width: 50%;
	      float: left;
	      background-color: #b4b472;
	      height: 100%;
	    }
	    & .right{
	      width: 50%;
	      float: left;
	      background-color: springgreen;
	      height: 100%;
	    }
	  }
	}



第三步：媒介查询-Media queries

	//小于620px
	@media screen and (max-width : 620px){
	  body{
	    background-color: red !important;
	  }
	}
	
	//大于620px 小于1024px
	@media screen and (min-width: 620px) and (max-width: 1024px){
	  body{
	  background-color: blue !important;
	  } 
	}

//附上自己公司之前的相应方式与更好的优化方式

公司写法：

	<head>
	    <meta charset="utf-8"/>
	    <script>
	        var phoneWidth = parseInt(window.screen.width);
	        var phoneScale = phoneWidth / 640 ;
	        document.write('<meta name="viewport" content="width=640, initial-scale = ' + phoneScale + ', maximum-scale = ' + phoneScale + ', user-scalable=no target-densitydpi=device-dpi">');
	    </script>
	    <meta name="format-detection" content="telephone=no">
	    <meta name="apple-mobile-web-app-capable" content="yes" />
	    <meta name="apple-mobile-web-app-status-bar-style" content="black" />
	    <title>详情</title>
	    <link href="<%=path %>/coach/v200/css/main.css" rel="stylesheet">
	    <link href="<%=path %>/coach/v300/css/banner-detail.css" rel="stylesheet">
	</head>

更好的写法：

	<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width,minimum-scale=1.0,maximum-scale=1.0,user-scalable=no"/>
    <meta content="telephone=no" name="format-detection">
    <meta content="email=no" name="format-detection">
    <meta name="apple-mobile-web-app-capable" content="yes" />
    <meta name="apple-mobile-web-app-status-bar-style" content="black" />
    <title>邀请教练</title>
    <link rel="stylesheet" href="<%=path%>/coach/v320/inviteCoach/inviteCoach.css?t=20160725"/>
	</head>

