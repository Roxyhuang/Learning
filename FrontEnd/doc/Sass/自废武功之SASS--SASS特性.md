自废武功之SASS--SASS特性
--
> 引用自 http://www.hubwiz.com/class/565c0c2abc27d77730c072b3

**一、选择器占位符%placeholder**

　　从sass 3.2.0以后就可以定义占位选择器%。这种选择器的优势在于：如果不调用则不会有任何多余的css文件，避免了以前在一些基础的文件中预定义了很多基础的样式，然后实际应用中不管是否使用了@extend去继承相应的样式，都会解析出来所有的样式。占位选择器以%标识定义，通过@extend调用。


	%mar {
	  margin: 5px;
	}
	%pad{
	  padding: 5px;
	}

这段代码没有被 @extend 调用，他并没有产生任何代码块，只是静静的躺在你的某个 SCSS 文件中。只有通过 @extend 调用才会产生代码：

	//SCSS
	%mar {
	  margin: 5px;
	}
	%pad{
	  padding: 5px;
	}
	 
	.btn {
	  @extend %mar;
	  @extend %pad;
	}
	 
	.block {
	  @extend %mar;
	 
	  span {
	    @extend %pad;
	  }
	}


编译出来的CSS

	//CSS
	.btn, .block {
	  margin-top: 5px;
	}
	 
	.btn, .block span {
	  padding-top: 5px;
	}


从编译出来的 CSS 代码可以看出，通过 @extend 调用的占位符，编译出来的代码会将相同的代码合并在一起。

**二、数据类型**



SassScript 支持六种主要的数据类型：

数字（例如 1.2、13、10px）  
文本字符串，无论是否有引号（例如 "foo"、'bar'、baz）  
颜色（例如 blue、#04a3f9、rgba(255, 0, 0, 0.5)）  
布尔值（例如 true、false）  
空值（例如 null）  
值列表，用空格或逗号分隔（例如 1.5em 1em 0 2em、Helvetica,   Arial, sans-serif）

SassScript 还支持所有其他 CSS 属性值类型， 例如 Unicode 范围和 !important 声明。 然而，它不会对这些类型做特殊处理。 它们只会被当做不带引号的字符串看待。



**三、字符串**

CSS 提供了两种类型的字符串：

　　带引号的字符串，例如 "Lucida Grande" 或 'http://sass-lang.com'；
不带引号的字符串，例如 sans-serif 或 bold。
编译 CSS 文件时不会改变其类型。只有一种情况例外，使用 #{ }插值语句 (interpolation) 时，有引号字符串将被编译为无引号字符串，这样方便了在混合指令 (mixin) 中引用选择器名。

	
	 @mixin firefox-message($selector) {
	  body.firefox #{$selector}:before {
	    content: "Hi, hubwiz users!";
	  }
	}
	 
	 @include firefox-message(".header");

被编译为：

	body.firefox .header:before {
	  content: "Hi, hubwiz users!"; }


注意：当 deprecated = property syntax 时，所有的字符串都将被编译为无引号字符串，不论是否使用了引号。