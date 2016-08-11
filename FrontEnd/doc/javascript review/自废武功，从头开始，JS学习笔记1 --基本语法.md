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

	var str = `hello world`;
	var str1 = str.indexOf('llo');
	var str2 = str.indexOf(`oll`);
	console.log(str1); //2
	console.log(str2); //-1

**(4)substring**

	var s = 'hello, world'
	s.substring(0, 5); // 从索引0开始到5（不包括5），返回'hello'
	s.substring(7); // 从索引7开始到结束，返回'world'


**三、数组相关 ：**

**(1)数组长度length属性：**

	var arr = [1, 2, 3.14, 'Hello', null, true];
	arr.length; // 6

**(2)改变length属性**

直接给Array的length赋一个新的值会导致Array大小的变化：
	
	var arr = [1,2,3];
	arr.length  //3;
	arr.length = 2  //2;
	arr   //[1, 2]

Array可以通过索引把对应的元素修改为新的值，因此，对Array的索引进行赋值会直接修改这个Array：


	arr.length = 4; //4;
	arr //[1, 2, undefined × 2];





请注意，如果通过索引赋值时，索引超过了范围，同样会引起Array大小的变化：﻿
	var arr = [`a`,`b`,`c`]
	
	arr[1] //"b"
	
	arr[2] //"c"




	var a = ["1",2,4,5,6,"b"]
	var a.length  //6	
	
	a[10]="a" //["1", 2, 4, 5, 6, "b", undefined × 4, "a"]


　　大多数其他编程语言不允许直接改变数组的大小，越界访问索引会报错。然而，JavaScript的Array却不会有任何错误。在编写代码时，不建议直接修改Array的大小，访问索引时要确保索引不会越界。



**(3)indexOf**

与String类似，Array也可以通过indexOf()来搜索一个指定的元素的位置：

	var arr = [10, 20, '30', 'xyz'];
	arr.indexOf(10); // 元素10的索引为0
	arr.indexOf(20); // 元素20的索引为1
	arr.indexOf(30); // 元素30没有找到，返回-1
	arr.indexOf('30'); // 元素'30'的索引为2
	
	//注意了，数字30和字符串'30'是不同的元素。


**(4)slice**

slice()就是对应String的substring()版本，它截取Array的部分元素，然后返回一个新的Array：


	var arr  =  [`a`,`b`,`c`,`d`];
	
	var subArr1 = arr.slice(0,2);
	
	var subArr2 = arr.slice(1);
	
	console.log(arr);  //["a", "b", "c", "d"]
	
	console.log(subArr1);  //["a", "b"]
	
	console.log(subArr2)   //["b", "c", "d"]


**(5) push和pop**
	
push()向Array的末尾添加若干元素，pop()则把Array的最后一个元素删除掉：	

	var arr = [1,2,3,4,5,6,7,8];
	undefined
	arr.push(`a`);
	9
	arr.push(`b`);
	10
	arr
	[1, 2, 3, 4, 5, 6, 7, 8, "a", "b"]
	arr.pop();
	"b"
	arr
	[1, 2, 3, 4, 5, 6, 7, 8, "a"]


	var arr = [1, 2];
	arr.push('A', 'B'); // 返回Array新的长度: 4
	arr; // [1, 2, 'A', 'B']
	arr.pop(); // pop()返回'B'
	arr; // [1, 2, 'A']
	arr.pop(); arr.pop(); arr.pop(); // 连续pop 3次
	arr; // []
	arr.pop(); // 空数组继续pop不会报错，而是返回undefined
	arr; // []


**(6)unshift和shift**


　　如果要往Array的头部添加若干元素，使用unshift()方法，shift()方法则把Array的第一个元素删掉：

	//实例1
	var arr =  [1,2]
	undefined
	arr.unshift('1',1)
	4
	arr 
	["1", 1, 1, 2]
	arr.shift()
	"1"
	arr
	[1, 1, 2]


	//实例2
	var arr = [1, 2];
	arr.unshift('A', 'B'); // 返回Array新的长度: 4
	arr; // ['A', 'B', 1, 2]
	arr.shift(); // 'A'
	arr; // ['B', 1, 2]
	arr.shift(); arr.shift(); arr.shift(); // 连续shift 3次
	arr; // []
	arr.shift(); // 空数组继续shift不会报错，而是返回undefined
	arr; // []

**(7)sort**

  专门会开一篇文章说


**(8)reverse**﻿

reverse()把整个Array的元素给掉个个，也就是反转：
	
	var arr = ['one', 'two', 'three'];
	arr.reverse(); 
	arr; // ['three', 'two', 'one']

**(9)splice**

splice()方法是修改Array的“万能方法”，它可以从指定的索引开始删除若干元素，然后再从该位置添加若干元素：


	var arr =  [`1`,`2`,`3`,`4`];   //undefined
	arr.splice(0,1,`2`)             //["1"]
	arr                             //["2", "2", "3", "4"]
	arr.splice(0,1);  				//["2"]
	arr								//["2", "3", "4"]
	arr.splice(0,0,'1')				//[]
	arr								//["1", "2", "3", "4"]

**(10)concat**

　　concat()方法把当前的Array和另一个Array连接起来，并返回一个新的Array：

	var arr = [`a`,`b`,`c`]；
	var added = arr.concat([1,2,3]);
	added //["a", "b", "c", 1, 2, 3]；


	请注意，concat()方法并没有修改当前Array，而是返回了一个新的Array。
	
	实际上，concat()方法可以接收任意个元素和Array，并且自动把Array拆开，然后全部添加到新的Array里：
	
	var arr = ['A', 'B', 'C'];
	arr.concat(1, 2, [3, 4]); // ['A', 'B', 'C', 1, 2, 3, 4]

**(11)join**

　　join()方法是一个非常实用的方法，它把当前Array的每个元素都用指定的字符串连接起来，然后返回连接后的字符串：


	var arr = [`a`,`b`,`c`];
	arr.join(`-`);
	"a-b-c"

如果Array的元素不是字符串，将自动转换为字符串后再连接。

**(12)多维数组**


如果数组的某个元素又是一个Array，则可以形成多维数组，例如：

var arr = [[1, 2, 3], [400, 500, 600], '-'];
上述Array包含3个元素，其中头两个元素本身也是Array。

实例：调用多维数组里的值

	var arr = [[1,2,33],[1,2],'-'] 
	arr[0][2]  //33

	arr.sort();
	alert('欢迎'+arr.slice(0, arr.length - 1).join(',')+'和'+arr.pop()+'同学！');·