自废武功，从头开始，JS学习笔记7 --高级函数相关
--

**一、高阶函数英文叫Higher-order function。那么什么是高阶函数？**

　　JavaScript的函数其实都指向某个变量。既然变量可以指向函数，函数的参数能接收变量，那么一个函数就可以接收另一个函数作为参数，这种函数就称之为高阶函数。

例子：
	// 定义add函数
	function add (x,y,f){
    return f(x) + f(y);
	}
	
	//定义abs方法
	function abs(i){

   	return Math.abs(i)  
	}

	add(12,100,abs);  //运行结果112

**二、Map**

由于map()方法定义在JavaScript的Array中，我们调用Array的map()方法，传入我们自己的函数，就得到了一个新的Array作为结果：

	function pow(x){
	   return x * x
	}
	
	
	var arr = [1,2,3,4,5,6,7,1,2,312];
	
	var mapArr = arr.map(pow)；
	
	mapArr //[1, 4, 9, 16, 25, 36, 49, 1, 4, 97344]


所以，map()作为高阶函数，事实上它把运算规则抽象了，因此，我们不但可以计算简单的f(x)=x2，还可以计算任意复杂的函数，比如，把Array的所有数字转为字符串：
	

	//Number转String 
	var arr = [1,2,3,4,5];
	arr.map(String) //["1", "2", "3", "4", "5"]


	//String转Number
	var arrStr = ["1", "2", "3", "4", "5"]
	arrStr.map(Number);
	[1, 2, 3, 4, 5]


**三、reduce**


　　再看reduce的用法。Array的reduce()把一个函数作用在这个Array的[x1, x2, x3...]上，这个函数必须接收两个参数，reduce()把结果继续和序列的下一个元素做累积计算，其效果就是：


	[x1, x2, x3, x4].reduce(f) = f(f(f(x1, x2), x3), x4)


比方说对一个Array求和，就可以用reduce实现：

	var arr = [1, 3, 5, 7, 9];
	arr.reduce(function (x, y) {
	    return x + y;
	}); // 25