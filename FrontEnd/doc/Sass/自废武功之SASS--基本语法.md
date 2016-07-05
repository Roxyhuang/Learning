自废武功之SASS--基本语法
--
> 引用汇智网sass教程

**一、声明变量：**

Sass 的变量包括三个部分：

1.声明变量的符号“$”  
2.变量名称  
3.赋予变量的值  

	$wdith:100px;
	$bgColor:#FFF;

例子：

	$width: 360px; 
	$height:40px;
	$border:1px solid red; 
	$color:blue;
	.box1 { 
		width: $width; 
		height:$height;
		border:$border;
	  	color:$color;
	}
	.box2{
		width: $width; 
		border:$border;
	  	color:$color;
	}


**二、变量的引用：**

　　凡是css属性的标准值（比如说1px或者bold）可存在的地方，变量就可以使用。css生成时，变量会被它们的值所替代。之后，如果你需要一个不同的值，只需要改变这个变量的值，则所有引用此变量的地方生成的值都会随之改变。

例子：

	$width: 360px; 
	$height:40px;
	$color: blue;
	$border: 1px solid $color; 
	.box1 { 
		width: $width; 
		height:$height;
		border:$border; 
	}
	.box2{
		width: $width; 
		border: $border; 
	  	background-color:$color;
	}


三、**普通变量与默认变量：**

1.普通变量

定以后可以在全局范围内使用。

	$color: #F90;
	.box2 {
	  border: 1px solid $color;
	}

2.默认变量

sass的默认变量仅需要在值后面加上!default即可。


	$baseHeight:        1.6 !default;
	body{
	    line-height: $baseHeight; 
	}

　　sass的默认变量一般是用来设置默认值，然后根据需求来覆盖的，只需要在默认变量之前重新声明下变量，重新赋值即可

	$baseHeight:        2;
	$baseHeight:        1.6 !default;
	body{
	    line-height: $baseHeight; 
	}

　　可以看出现在编译后的line-height为2，而不是我们默认的1.6。默认变量的价值在进行组件化开发的时候会非常有用。


**四、局部变量和全局变量：**


　　从 3.4 版本开始，Sass 已经可以正确处理作用域的概念，并通过创建一个新的局部变量来代替。

例子

	//SCSS
	$color: blue !default;//定义全局变量(在选择器、函数、混合宏...的外面定义的变量为全局变量)
	.box1 {
	  color: $color;//调用全局变量
	}
	p {
	  $color: red;//定义局部变量
	  a {
	    color: $color;//调用局部变量
	  }
	}
	.box2 {
	  color: $color;//调用全局变量
	}


css 的结果：

	//CSS
	.box1 {
	  color: blue;
	}
	p a {
	  color: red;
	}
	.box2 {
	  color: blue;
	}


$color 就是一个全局变量，而定义在元素内部的变量，比如 $color:red; 是一个局部变量。

除此之外，Sass 现在还提供一个 !global 参数。!global 和 !default 对于定义变量都是很有帮助的。

现在我们来试试 !global 参数


	//SCSS
	$color: blue ;
	.stage {
	  color: $color;
	}
	p {
	  $color: red !global;
	  a {
	    color: $color;
	  }
	}
	div {
	  color: $color;
	}


**五、嵌套-选择器嵌套：**


　　所谓选择器嵌套指的是在一个选择器中嵌套另一个选择器来实现继承，从而增强了sass文件的结构性和可读性。

  在选择器嵌套中，可以使用&表示父元素选择器。


**Sass style**

	#top_nav{
	  line-height: 40px;
	  li{
	float:left;
	  }
	  a{
	padding: 0 10px;
	color: #fff;
	 
	&:hover{
	  color:#ddd;
	}
	  }
	}

**CSS style**

	#top_nav{
	  line-height: 40px;
	}
	#top_nav li{
	    float:left;
	}
	#top_nav a{
	    padding: 0 10px;
	    color: #fff;
	}
	#top_nav a:hover{
	      color:#ddd;
	}


**六、嵌套-属性嵌套**

Sass语法：

	.box2 {
	  border: {
	    style: solid;
	    left: {
	      width: 4px;
	      color: #888;
	    }
	    right: {
	      width: 2px;
	      color: #ccc;
	    }
	  }
	}

编译后的CSS：

	.box2 {
	  border-style: solid;
	  border-left-width: 4px;
	  border-left-color: #888;
	  border-right-width: 2px;
	  border-right-color: #ccc; 
	}