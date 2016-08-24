自废武功，从头开始，JS学习笔记10 --generator
--

**一、generator**


　　generator（生成器）是ES6标准引入的新的数据类型。一个generator看上去像一个函数，但可以返回多次。


我们先复习函数的概念。一个函数是一段完整的代码，调用一个函数就是传入参数，然后返回结果：


	function foo(x) {
	    return x + x;
	}
	
	var r = foo(1); // 调用foo函数


函数在执行过程中，如果没有遇到return语句（函数末尾如果没有return，就是隐含的return undefined;），控制权无法交回被调用的代码。


generator跟函数很像，定义如下：


	function* foo(x) {
	    yield x + 1;
	    yield x + 2;
	    return x + 3;
	}