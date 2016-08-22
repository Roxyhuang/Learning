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



**四、filter**

filter也是一个常用的操作，它用于把Array的某些元素过滤掉，然后返回剩下的元素。


	var arr =[1,2,3,4]
	arr.filter((x)=>x!=2) //[1, 3, 4]


	var arr = ['A', '', 'B', null, undefined, 'C', '  '];
	var r = arr.filter(function (s) {
	    return s && s.trim(); // 注意：IE9以下的版本没有trim()方法
	});
	r; // ['A', 'B', 'C']

**五、sort**

通常规定，对于两个元素x和y，**如果认为x < y，则返回-1，如果认为x == y，则返回0，如果认为x > y，则返回1**，这样，排序算法就不用关心具体的比较过程，而是根据比较结果直接排序。


JavaScript的Array的sort()方法就是用于排序的，但是排序结果可能让你大吃一惊：


	// 看上去正常的结果:
	['Google', 'Apple', 'Microsoft'].sort(); // ['Apple', 'Google', 'Microsoft'];
	
	// apple排在了最后:
	['Google', 'apple', 'Microsoft'].sort(); // ['Google', 'Microsoft", 'apple']
	
	// 无法理解的结果:
	[10, 20, 1, 2].sort(); // [1, 10, 2, 20]


第二个排序把apple排在了最后，是因为字符串根据ASCII码进行排序，而小写字母a的ASCII码在大写字母之后。

第三个排序结果是什么鬼？简单的数字排序都能错？

**这是因为Array的sort()方法默认把所有元素先转换为String再排序，结果'10'排在了'2'的前面，因为字符'1'比字符'2'的ASCII码小。**



如果不知道sort()方法的默认排序规则，直接对数字排序，绝对栽进坑里！

幸运的是，sort()方法也是一个高阶函数，它还可以接收一个比较函数来实现自定义的排序。




**要按数字大小排序，我们可以这么写：**

    //升序
	sortArr.sort(function(x,y){
	    if(x>y){
	      return 1;
	     
	    }
	     if(x<y){
	      return -1;
	    }
	    
	   return 0 ;
	
	})
	[10, 43, 99, 1003]



如果要倒序排序，我们可以把大的数放前面：


	//倒序
	sortArr.sort(function(x,y){
	    if(x>y){
	      return -1;
	     
	    }
	     if(x<y){
	      return 1;
	    }
	    
	   return 0 ;
	
	})
	[1003, 99, 43, 10]


默认情况下，对字符串排序，是按照ASCII的大小比较的，现在，我们提出排序应该忽略大小写，按照字母序排序。要实现这个算法，不必对现有代码大加改动，只要我们能定义出忽略大小写的比较算法就可以：

	var arr = ['Google', 'apple', 'Microsoft'];
	arr.sort(function (s1, s2) {
	    x1 = s1.toUpperCase();
	    x2 = s2.toUpperCase();
	    if (x1 < x2) {
	        return -1;
	    }
	    if (x1 > x2) {
	        return 1;
	    }
	    return 0;
	}); // ['apple', 'Google', 'Microsoft']







忽略大小写来比较两个字符串，实际上就是先把字符串都变成大写（或者都变成小写），再比较。

从上述例子可以看出，高阶函数的抽象能力是非常强大的，而且，核心代码可以保持得非常简洁。

最后友情提示，sort()方法会直接对Array进行修改，它返回的结果仍是当前Array：
	
	var a1 = ['B', 'A', 'C'];
	var a2 = a1.sort();
	a1; // ['A', 'B', 'C']
	a2; // ['A', 'B', 'C']
	a1 === a2; // true, a1和a2是同一对象