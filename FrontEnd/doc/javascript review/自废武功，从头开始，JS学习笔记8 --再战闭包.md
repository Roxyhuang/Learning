自废武功，从头开始，JS学习笔记8 --再战闭包


**一、函数作为返回值**


高阶函数除了可以接受函数作为参数外，还可以把函数作为结果值返回。

我们来实现一个对Array的求和。通常情况下，求和的函数是这样定义的：


	function sum(arr) {
	    return arr.reduce(function (x, y) {
	        return x + y;
	    });
	}
	
	sum([1, 2, 3, 4, 5]); // 15

但是，如果不需要立刻求和，而是在后面的代码中，根据需要再计算怎么办？可以不返回求和的结果，而是返回求和的函数！

	function lazy_sum(arr) {
	    var sum = function () {
	        return arr.reduce(function (x, y) {
	            return x + y;
	        });
	    }
	    return sum;
	}


当我们调用lazy_sum()时，返回的并不是求和结果，而是求和函数：


	var f = lazy_sum([1, 2, 3, 4, 5]); // function sum()


调用函数f时，才真正计算求和的结果：

	f(); // 15


在这个例子中，我们在函数lazy_sum中又定义了函数sum，并且，内部函数sum可以引用外部函数lazy_sum的参数和局部变量，当lazy_sum返回函数sum时，相关参数和变量都保存在返回的函数中，这种称为“闭包（Closure）”的程序结构拥有极大的威力。

请再注意一点，当我们调用lazy_sum()时，每次调用都会返回一个新的函数，即使传入相同的参数：

	var f1 = lazy_sum([1, 2, 3, 4, 5]);
	var f2 = lazy_sum([1, 2, 3, 4, 5]);
	f1 === f2; // false
	f1()和f2()的调用结果互不影响。


**二、闭包**

注意到返回的函数在其定义内部引用了局部变量arr，所以，当一个函数返回了一个函数后，其内部的局部变量还被新函数引用，所以，闭包用起来简单，实现起来可不容易。

另一个需要注意的问题是，返回的函数并没有立刻执行，而是直到调用了f()才执行。我们来看一个例子：
	
	function count() {
	    var arr = [];
	    for (var i=1; i<=3; i++) {
	        arr.push(function () {
	            return i * i;
	        });
	    }
	    return arr;
	}
	
	var results = count();
	var f1 = results[0];
	var f2 = results[1];
	var f3 = results[2];

	f1(); // 16
	f2(); // 16
	f3(); // 16


可以这样写：


	function count() {
	    var arr = [];
	    for (var i=1; i<=3; i++) {
	        arr.push((function (n) {
	            return function () {
	                return n * n;
	            }
	        })(i));
	    }
	    return arr;
	}
	
	var results = count();
	var f1 = results[0];
	var f2 = results[1];
	var f3 = results[2];
	
	f1(); // 1
	f2(); // 4
	f3(); // 9



通常，一个立即执行的匿名函数可以把函数体拆开，一般这么写：

	(function (x) {
	    return x * x;
	})(3);