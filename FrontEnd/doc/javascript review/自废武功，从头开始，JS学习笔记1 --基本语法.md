自废武功，从头开始，JS学习笔记1 --数据类型和变量
--
> 本笔记主要是学习http://www.liaoxuefeng.com/wiki/001434446689867b27157e896e74d51a89c25cc8b43bdb3000的笔记

**一、数据类型：**


JS几种基本数据类型：

(1) Number

(2) String

(3) Boolean

(4) null

(5) undefined

(6) Array

(7) Object


**1.Number：**

　　JavaScript不区分整数和浮点数，统一用Number表示，以下都是合法的Number类型：

	123; // 整数123
	0.456; // 浮点数0.456
	1.2345e3; // 科学计数法表示1.2345x1000，等同于1234.5
	-99; // 负数
	NaN; // NaN表示Not a Number，当无法计算结果时用NaN表示
	Infinity; // Infinity表示无限大，当数值超过了JavaScript的Number所能表示的最大值时，就表示为Infinity
	
　　计算机由于使用二进制，所以，有时候用十六进制表示整数比较方便，十六进制用0x前缀和0-9，a-f表示，例如：0xff00，0xa5b4c3d2，等等，它们和十进制表示的数值完全一样。

Number可以直接做四则运算，规则和数学一致：

**2.String**



