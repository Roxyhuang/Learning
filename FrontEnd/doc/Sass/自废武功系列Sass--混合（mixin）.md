自废武功系列Sass--混合（mixin）
--
> 引用自汇智网

**一、混合声明和调用：**


　　SASS中使用mixin声明混合，可以传递参数，参数名以$符号开始，多个参数以逗号分开，也可以给参数设置默认值。
我经常用这个方式来写浏览器之间的兼容

声明的@mixin通过@include来调用。

在 Sass 中，使用“@mixin”来声明一个混合宏。如：

	 @mixin border-radius{
	    -webkit-border-radius: 5px;
	    border-radius: 5px;
	}

其中 @mixin 是用来声明混合宏的关键词，有点类似 CSS 中的 @media、@font-face 一样。border-radius 是混合宏的名称。大括号里面是复用的样式代码。

在一个按钮中要调用定义好的混合宏“border-radius”，可以这样使用：


	button {
	    @include border-radius;
	}


这个时候编译出来的 CSS:


	button {
	  -webkit-border-radius: 5px;
	  border-radius: 5px;
	}


**二、无参数mixin：**


Sass 的混合宏有一个强大的功能，可以无参，可以传参，那么在 Sass 中我们先来学习下

在混合宏中，可以传一个不带任何值的参数，比如：

	@mixin center-block {
	    margin-left:auto;
	    margin-right:auto;
	}

在混合宏“center-block”中定义了无参数。

调用混合宏：

	.box2{
	    @include center-block;
	}

编译出来的 CSS:

	.box2{
	    margin-left:auto;
	    margin-right:auto;
	}


**三、有参数mixin：**

在 Sass 的混合宏中，还可以给混合宏的参数传一个默认值，例如：

	@mixin opacity($opacity:50){
	  opacity:$opacity/100;
	  filter: alpha(opacity=$opacity);
	}
	
	#div{
	  @include opacity(10);
	}

在混合宏“opacity”传了一个参数“$opacity”，而且给这个参数赋予了一个默认值“50”。

在调用类似这样的混合宏时，假设你的页面中的圆角很多地方都是需要的，那么这个时候只需要调用默认的混合宏“opacity”:

	$width: 360px; 
	$color: #F90 !default;
	$border: 1px solid #5bc0de; 
	 @mixin opacity($opacity:50) {
	  opacity: $opacity / 100;
	  filter: alpha(opacity=$opacity);
	}
	@mixin radius($radius:3px){
	  -webkit-border-radius:$radius;
	  border-radius: $radius; 
	}
	.box2{
		width: $width; 
		border: $border; 
	    color: $color;
	    @include opacity;
	  	@include radius(20px)
	}


**四、多个参数mixin**

调用时可直接传入值，如@include传入参数的个数小于@mixin定义参数的个数，则按照顺序表示，后面不足的使用默认值，如不足的没有默认值则报错。

除此之外还可以选择性的传入参数，使用参数名与值同时传入。


例子：

	$width: 360px; 
	$color: #F90 !default;
	 @mixin horizontal-line($border:1px dashed #5bc0de, $padding:10px){
	    border-bottom:$border;
	    padding-top:$padding;
	    padding-bottom:$padding;  
	}
	@mixin boxSize($width:100px,$height:200px){
		width:$width;
	  	height:$height;
	}
	.box2{
		width: $width;
	    color: $color;
	    @include horizontal-line(1px solid #5bc0de);
	    @include horizontal-line($padding:15px);
	}
	.box1{
		@include boxSize(10px,10px)
	}


**五、多组值参数mixin**

如果一个参数可以有多组值，如box-shadow、transition等，那么参数则需要在变量后加三个点"..."表示，如$variables...。

box-shadow可以有多组值，所以在变量参数后面添加...
	
	@mixin box-shadow($shadow...) {
	  -webkit-box-shadow:$shadow;
	  box-shadow:$shadow;
	}


在实际调用中：

	.box{
	  border:1px solid #ccc;
	  @include box-shadow(0 2px 2px rgba(0,0,0,.3),0 3px 3px rgba(0,0,0,.3),0 4px 4px rgba(0,0,0,.3));
	}

编译出来的CSS:

	.box{
	  border:1px solid #ccc;
	  -webkit-box-shadow:0 2px 2px rgba(0,0,0,.3),0 3px 3px rgba(0,0,0,.3),0 4px 4px rgba(0,0,0,.3);
	  box-shadow:0 2px 2px rgba(0,0,0,.3),0 3px 3px rgba(0,0,0,.3),0 4px 4px rgba(0,0,0,.3);
	}