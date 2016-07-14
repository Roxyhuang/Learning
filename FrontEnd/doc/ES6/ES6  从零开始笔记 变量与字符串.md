ES6  从零开始笔记 变量与字符串
--
> 引用自汇智网教程

**一、let：**

let是ES6中新增关键字。

它的作用类似于var，用来声明变量，但是所声明的变量，只在let命令所在的代码块内有效。

	
	if(true){
	    var a = 1;
	    let b = 2;
	}
	document.write(a);
	document.write(b);  // 报错：ReferenceError: b is not defined

体会下let和var的作用域范围:

	function f1() {
	  var a = 8;
	  let n = 5;
	  if (true) {
	      let n = 10;
	      var a = 20
	  }
	  document.write(n); // 5
	  document.write(a); // 20
	}
	f1();


**二、let应用：**

for循环的计数器，就很合适使用let命令。


	var a = [];
	for (let i = 0; i < 10; i++) {
	  a[i] = function () {
	    document.write(i);
	  };
	}
	document.write(a[6]()); 


for循环的计数器，就很合适使用let命令。



**三、const命令：**

const 声明的是常量，一旦声明，值将是不可变的

	const PI = 3.1415;
	PI // 3.1415
	 
	PI = 3;
	PI // 3.1415
	 
	const PI = 3.1;
	PI // 3.1415


const 也具有块级作用域

	if (true) {
	  const max = 5;
	}
	document.write(max);  // ReferenceError 常量MAX在此处不可得 


const 不能变量提升（必须先声明后使用）

	if (true) {
	  document.write(MAX); // ReferenceError
	  const MAX = 5;
	}

const 不可重复声明

	var message = "Hello!";
	let age = 25;
	 
	// 以下两行都会报错
	const message = "Goodbye!";
	const age = 30;



