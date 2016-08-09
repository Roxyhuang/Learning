自废武功，从头开始，JS学习笔记1 --基本语法相关
--
> 本笔记主要是学习http://www.liaoxuefeng.com/wiki/001434446689867b27157e896e74d51a89c25cc8b43bdb3000的笔记

吾辈这次准备重新看两次JS，先快速浏览一次廖雪峰的JS教程，再静下心来，好好看看js权威指南，现在不是先从数据类型开始研究吧



**一、数据类型：**


JS几种基本数据类型：

(1) Number

(2) String

(3) Boolean

(4) null

(5) undefined

(6) Object （包括Array）


**二、 字符串相关：**

**1、普通字符串：**

	//双引号
	"I'm a man!!!"
	//单引号	
	'I'm a man too!!!'


**2、转义字符：**

如果字符串内部既包含'又包含"怎么办？可以用转义字符\来标识，比如：
	
	//转移字符
	//    \'来代表一个字符
	console.log("I\'m \"OK\"");


**3、ASCII+Unicode字符：**

\x##形式的十六进制表示，例如：

	'\x41'; // 完全等同于 'A'

还可以用\u####表示一个Unicode字符：

	'\u4e2d\u6587'; // 完全等同于 '中文'

**4、ES6多行字符串：**
	
	`
	多行字符串
	多行字符串
	多行字符串
	`

**5、模板字符串：**

es5:
	
	var name = '小猴';
	var age = 25;
	var message ='你好'+name+',你今年'+age+'岁'//"你好小猴,你今年25岁"


es6:

	var name = '小猴';
	var age = 25;
	var message = `你好${name},你今年${age}岁`//"你好小猴,你今年25岁"


**6、操作字符串：**

	//字符串长度
	var s = 'Hello'
	s.length;

	//字符串索引
	var s = 'Hello,world';

	s[0]; // 'H'
	s[6]; // ' '
	s[7]; // 'w'
	s[12]; // '!'
	s[13]; // undefined 超出范围的索引不会报错，但一律返回undefined

> 需要特别注意的是，字符串是不可变的，如果对字符串的某个索引赋值，不会有任何错误，但是，也没有任何效果：

	var s = 'Test';
	s[0] = 'X';
	alert(s); // s仍然为'Test'


> JavaScript为字符串提供了一些常用方法，注意，调用这些方法本身不会改变原有字符串的内容，而是返回一个新字符串：

**(1)toUpperCase**

toUpperCase()把一个字符串全部变为大写：

	var a = `aaaa`;
	a.toUpperCase();  //"DDASDADA"
	a  //"ddasdada"

**(2)toLowerCase()**

toLowerCase()把一个字符串全部变为小写：

	var b = `BBBbb`;
	b.toLowerCase(); //"bbbbb"
	b //"BBBbb"


**(3)indexOf**

indexOf()会搜索指定字符串出现的位置：