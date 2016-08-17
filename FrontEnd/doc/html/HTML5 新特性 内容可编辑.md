HTML5 新特性 内容可编辑 contenteditable  
--
> http://blog.163.com/hongshaoguoguo@126/blog/static/18046981201322310046403?suggestedreading

　　新的浏览器拥有一个可以应用于元素中的漂亮的新属性，这就是contenteditable。就像名字所表示的，它允许用户去改变元素中包含的任何文字，包括它的子对象。这个属性的用途很多，包括简单的to-do list应用。

	<!DOCTYPE html>
	<html>
	<head>
	    <meta charset="utf-8">
	    <title>contenteditable</title>
	</head>
	<body>
	<h2 contenteditable="true"> To-Do List </h2>
	<ul contenteditable="true">
	    <li> 123456</li>
	    <li> 456789</li>
	    <li> 789123 </li>
	</ul>
	</body>
	</html>