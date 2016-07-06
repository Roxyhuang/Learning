自废武功系列--运算
--
> 引用汇智网 http://www.hubwiz.com/class/565c0c2abc27d77730c072b3
f

**一、数字运算：**


　　所有数据类型都支持等式运算 (== and !=)。 另外，每种数据类型也有其支持的特殊运算符。

　　SassScript 支持数字的标准运算（加 +、减 -、乘 *、除 /和取模 %），并且，如果需要的话，也可以在不同单位间做转换：

	p {
	  width: 1in + 8pt;
	}

被编译为：

	p {
	  width: 9in; 
	}

　　数字也支持关系运算（<、>、<=、>=）， 等式运算（==、!=）被所有数据类型支持。

**二、除法运算和：**

	
　　CSS 允许 / 出现在属性值里，作为分隔数字的一种方法。 既然 SassScript 是 CSS 属性语法的扩展， 他就必须支持这种语法，同时也允许 / 用在除法运算上。 也就是说，默认情况下，在 SassScript 里用 / 分隔的两个数字， 都会在 CSS 中原封不动的输出。

　　然而，在以下三种情况中，/ 会被解释为除法运算。 这就覆盖了绝大多数真正使用除法运算的情况。 这些情况是：

1.如果数值或它的任意部分是存储在一个变量中或是函数的返回值。

2.如果数值被圆括号包围。

3.如果数值是另一个数学表达式的一部分。

例如：

	p {
	  font: 10px/8px;             // 纯 CSS，不是除法运算
	  $width: 1000px;
	  width: $width/2;            // 使用了变量，是除法运算
	  width: round(1.5)/2;        // 使用了函数，是除法运算
	  height: (500px/2);          // 使用了圆括号，是除法运算
	  margin-left: 5px + 8px/2px; // 使用了加（+）号，是除法运算
	}

被编译为：

	p {
	  font: 10px/8px;
	  width: 500px;
	  height: 250px;
	  margin-left: 9px; 
	}
　
如果你希望在纯 CSS 中使用变量和 /， 你可以用 #{} 包住变量。 例如：

	p {
	  $font-size: 12px;
	  $line-height: 30px;
	  font: #{$font-size}/#{$line-height};
	}

被编译为：

	p {
	  font: 12px/30px; 
	}


**三、颜色运算：**


所有算数运算都支持颜色值， 并且是分段运算的。 也就是说，红、绿、蓝各颜色分量会单独进行运算。 例如：


	p {
	  color: #010203 + #040506;
	}

计算公式为 01 + 04 = 05、02 + 05 = 07 和 03 + 06 = 09， 并且被合成为：

	p {
	  color: #050709; 
	}

一般 {Sass::Script::Functions color functions} 比颜色运算更有用，并且能达到相同的效果。

算数运算也能将数字和颜色值一起运算，同样也是分段运算的。 例如：


	p {
	  color: #010203 * 2;
	}

计算公式为 01 * 2 = 02、02 * 2 = 04 和 03 * 2 = 06， 并且被合成为：


	p {
	  color: #020406;
	 }


**四、字符串运算：**

“+” 运算符可以用来连接字符串：

	
	p {
	  cursor: e + -resize;
	}

被编译为：

	p {
  	cursor: e-resize;
	}


注意，如果有引号的字符串被添加了一个没有引号的字符串 （也就是，带引号的字符串在 + 符号左侧）， 结果会是一个有引号的字符串。 同样的，如果一个没有引号的字符串被添加了一个有引号的字符串 （没有引号的字符串在 + 符号左侧）， 结果将是一个没有引号的字符串。 
**（总结下来跟着左边的！！！）**

	p:before {
	  content: "Foo " + Bar;
	  font-family: sans- + "serif";
	}

被编译为：

	p:before {
	  content: "Foo Bar";
	  font-family: sans-serif; 
	}


默认情况下，如果两个值彼此相邻，它们会被用空格连接起来：

	p {
	  margin: 3px + 4px auto;
	}	

被编译为：

	p {
  	margin: 7px auto; 
	}


在文本字符串中，#{} 形式的表达式可以被用来在字符串中添加动态值：

	p:before {
	  content: "I ate #{5 + 10} pies!";
	}


被编译为：

	p:before {
	  content: "I ate 15 pies!"; }


空值会被视作空字符串：

	$value: null;
	p:before {
	  content: "I ate #{$value} pies!";
	}


被编译为：

	p:before {
	  content: "I ate  pies!"; }