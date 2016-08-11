sessionStorage 的一个demo
--
>兼容方案https://segmentfault.com/q/1010000003969295
>http://www.cnblogs.com/jiujiaoyangkang/p/4998518.html

**sessionStorage.html：**

	<!DOCTYPE html>
	<html lang="en">
	<head>
	    <meta charset="UTF-8">
	    <title>Title</title>
	</head>
	<body>
	    <p>表单测试</p>
	    <form>
	        <label for="name">名称：</label><input  value="" id="name"/>
	        <label for="price">价格</label><input  value="" id="price"/>
	    </form>
	    <button id="next" onclick="nextClick()">下一步</button>
	</body>
	    <script src="../js/jquery-1.9.1.min.js"></script>
	    <script>
	        (function(){
	            if(sessionStorage.formData){
	                var JsonData = JSON.parse(sessionStorage.formData);
	                if(JsonData.name){
	                    document.getElementById("name").value = JsonData.name
	                }
	                if(JsonData.price){
	                    document.getElementById("price").value = JsonData.price
	                }
	            }else{
	
	            }
	
	        })();
	
	        function nextClick(){
	            var formData ={
	                name :document.getElementById("name").value,
	                price : document.getElementById("price").value
	            }
	            sessionStorage.formData = JSON.stringify(formData);
	            setTimeout(function(){
	                window.location.href = "sessionStorage2.html"
	            },100)
	        }
	    </script>
	</html>


**sessionStorage2.html：**

	<!DOCTYPE html>
	<html lang="en">
	<head>
	    <meta charset="UTF-8">
	    <title>Title</title>
	</head>
	<body>
	    <p>我已经是最终页面了</p>
	    <p>我的名称：</p><p id="name"></p>
	    <p>我的价格：</p><p id="price"></p>
	</body>
	<script>
	    (function(){
	        if(sessionStorage.formData){
	            var JsonData = JSON.parse(sessionStorage.formData);
	            if(JsonData.name){
	                document.getElementById("name").innerText = JsonData.name
	            }
	            if(JsonData.price){
	                document.getElementById("price").innerText = JsonData.price
	            }
	        }else{
	
	        }
	    })();
	</script>
	</html>