onbeforeunload以及unload 监听页面打开或者刷新状态
--
> http://www.runoob.com/jsref/event-onbeforeunload.html


**一、通过在body 添加onbeforeunload**
	
	<!DOCTYPE html>
	<html lang="en">
	<head>
	    <meta charset="UTF-8">
	    <title>Title</title>
	</head>
	<body onbeforeunload="return myFunction()">
	<a href="www.baidu.com">1111 </a>
	</body>
	<script>
	    function myFunction() {
	        return "我在这写点东西...";
	    }
	<script>

**二、通过addEventListener监听beforeunload**

	<!DOCTYPE html>
	<html lang="en">
	<head>
	    <meta charset="UTF-8">
	    <title>Title</title>
	</head>
	<body>
	<a href="www.baidu.com">1111 </a>
	</body>
	<script>

	window.addEventListener("beforeunload", function(event) {
        event.returnValue = "我在这写点东西...";
    });
	</script>

**三、JS中直接添加**

	<!DOCTYPE html>
	<html lang="en">
	<head>
	    <meta charset="UTF-8">
	    <title>Title</title>
	</head>
	<body>
	<a href="www.baidu.com">1111 </a>
	</body>
	<script>
	window.onbeforeunload = function(event) {
	    event.returnValue = "我在这写点东西...";
	};
	</script>