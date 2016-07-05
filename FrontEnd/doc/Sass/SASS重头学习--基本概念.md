SASS重头学习--基本概念
--
> 引用汇智网教程内容http://www.hubwiz.com/class/565c0c2abc27d77730c072b3

**一、什么Sass**

　　Sass是一门高于CSS的元语言，它能用来清洗地，结构化的描述文件样式，有着比普通CSS更强大的功能。  
　　Sass 是采用的Ruby语言编写的一款css预处理语言，它诞生于2007年，是最早成熟css预处理语言。最初它是为了配合haml而设计的，因此有着和haml一样的缩进式风格。  
　　Sass从第三代开始，放弃了缩进式风格，并且完全向下兼容普通的css代码，这一代的Sass也被称为Scss。

**二、Sass和SCSS有什么区别？**


1.文件扩展名不同，Sass是以.sass后缀为扩展名，而SCSS是以.scss后缀为扩展名  
2.语法书写方式不同，Sass是以严格的缩进式语法规则来书写，不带大括号{}和分号;，而SCSS的语法书写和我们的CSS语法书写方式非常类似。


Sass 语法：
	
	$font-stack: Helvetica, sans-serif  //定义变量
	$primary-color: #fff //定义变量
	 
	body
	  font: 100% $font-stack
	  color: $primary-color



SCSS 语法：
	
	$font-stack: Helvetica, sans-serif;
	$primary-color: #fff;
	 
	body {
	  font: 100% $font-stack;
	  color: $primary-color;
	}


编译出来的CSS：

	body {
	  font: 100% Helvetica, sans-serif;
	  color: #fff;
	}


**三、四种style生成后的css**

在 Sass 中编译出来的样式风格也可以按不同的样式风格显示。其主要包括以下几种样式风格：

1.  嵌套输出方式 **nested**
2.  展开输出方式 **expanded**
3.  紧凑输出方式 **compact**
4.  压缩输出方式 **compressed**

**原始代码**
	
		nav {
	  ul {
	    margin: 0;
	    padding: 0;
	    list-style: none;
	  }
	 
	  li { display: inline-block; }
	 
	  a {
	    display: block;
	    padding: 6px 12px;
	    text-decoration: none;
	  }
	}




**nested风格**

	nav ul {
		 margin: 0;
		 padding: 0;
		 list-style: none; }
	nav li {
		 display: inline-block; }
	nav a {
		 display: block;
		 padding: 6px 12px;
		 text-decoration: none; }


**expanded风格** 这个输出的 CSS 样式风格和 nested 类似，只是大括号在另起一行，同样上面的代码，编译出来：

	nav ul {
	  margin: 0;
	  padding: 0;
	  list-style: none;
	}
	nav li {
	  display: inline-block;
	}
	nav a {
	  display: block;
	  padding: 6px 12px;
	  text-decoration: none;
	}


**compact风格：**

	nav ul { margin: 0; padding: 0; list-style: none; }
	nav li { display: inline-block; }
	nav a { display: block; padding: 6px 12px; text-decoration: none; }


**compressed风格：**

	nav ul{margin:0;padding:0;list-style:none}nav li{display:inline-block}nav a{display:block;padding:6px 12px;text-decoration:none}

