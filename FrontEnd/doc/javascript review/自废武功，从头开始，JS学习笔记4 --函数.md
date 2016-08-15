自废武功，从头开始，JS学习笔记4 --函数
--
**一、函数的定义：**

在JavaScript中，定义函数的方式如下两种：

（1）函数声明：
	
	function abs(x) {
	    if (x >= 0) {
	        return x;
	    } else {
	        return -x;
	    }
	}

上述abs()函数的定义如下：

function指出这是一个函数定义；
abs是函数的名称；
(x)括号内列出函数的参数，多个参数以,分隔；
{ ... }之间的代码是函数体，可以包含若干语句，甚至可以没有任何语句。
请注意，函数体内部的语句在执行时，一旦执行到return时，函数就执行完毕，并将结果返回。因此，函数内部通过条件判断和循环可以实现非常复杂的逻辑。

如果没有return语句，函数执行完毕后也会返回结果，只是结果为undefined。

由于JavaScript的函数也是一个对象，上述定义的abs()函数实际上是一个函数对象，而函数名abs可以视为指向该函数的变量。

因此由下第二种方法

（2）函数表达式：


	var abs = function (x) {
	    if (x >= 0) {
	        return x;
	    } else {
	        return -x;
	    }
	};

在这种方式下，function (x) { ... }是一个匿名函数，它没有函数名。但是，这个匿名函数赋值给了变量abs，所以，通过变量abs就可以调用该函数。

上述两种定义完全等价，注意第二种方式按照完整语法需要在函数体末尾加一个;，表示赋值语句结束。


**二、函数调用**

调用函数时，按顺序传入参数即可：

	Math.abs(10) //10
	Math.abs(-9) //9

由于JavaScript允许传入任意个参数而不影响调用，因此传入的参数比定义的参数多也没有问题，虽然函数内部并不需要这些参数：

	abs(10, 'blablabla'); // 返回10
	abs(-9, 'haha', 'hehe', null); // 返回9

传入的参数比定义的少也没有问题：

	
	abs(); // 返回NaN

此时abs(x)函数的参数x将收到undefined，计算结果为NaN。

要避免收到undefined，可以对参数进行检查：

	function abs(x) {
	    if (typeof x !== 'number') {
	        throw 'Not a number';
	    }
	    if (x >= 0) {
	        return x;
	    } else {
	        return -x;
	    }
	}


**三、arguments**

JavaScript还有一个免费赠送的关键字arguments，它只在函数内部起作用，并且永远指向当前函数的调用者传入的所有参数。arguments类似Array但它不是一个Array：


        function foo(x){
            console.log(x);
            for(var i = 0 ; i<arguments.length;i++){
                console.log(arguments[i]);
            }
        }

        foo(10,20,30);


　　利用arguments，你可以获得调用者传入的所有参数。也就是说，即使函数不定义任何参数，还是可以拿到参数的值：


	
	function abs() {
	    if (arguments.length === 0) {
	        return 0;
	    }
	    var x = arguments[0];
	    return x >= 0 ? x : -x;
	}
	
	abs(); // 0
	abs(10); // 10
	abs(-9); // 9



实际上arguments最常用于判断传入参数的个数。你可能会看到这样的写法：

	// foo(a[, b], c)
	// 接收2~3个参数，b是可选参数，如果只传2个参数，b默认为null：
	function foo(a, b, c) {
	    if (arguments.length === 2) {
	        // 实际拿到的参数是a和b，c为undefined
	        c = b; // 把b赋给c
	        b = null; // b变为默认值
	    }
	    // ...
	}


要把中间的参数b变为“可选”参数，就只能通过arguments判断，然后重新调整参数并赋值。



**四、rest参数**

由于JavaScript函数允许接收任意个参数，于是我们就不得不用arguments来获取所有参数：

	function foo(a, b) {
	    var i, rest = [];
	    if (arguments.length > 2) {
	        for (i = 2; i<arguments.length; i++) {
	            rest.push(arguments[i]);
	        }
	    }
	    console.log('a = ' + a);
	    console.log('b = ' + b);
	    console.log(rest);
	}



由于JavaScript函数允许接收任意个参数，于是我们就不得不用arguments来获取所有参数：


为了获取除了已定义参数a、b之外的参数，我们不得不用arguments，并且循环要从索引2开始以便排除前两个参数，这种写法很别扭，只是为了获得额外的rest参数，有没有更好的方法？

ES6标准引入了rest参数，上面的函数可以改写为


	function foo(a, b, ...rest) {
	    console.log('a = ' + a);
	    console.log('b = ' + b);
	    console.log(rest);
	}
	
	foo(1, 2, 3, 4, 5);
	// 结果:
	// a = 1
	// b = 2
	// Array [ 3, 4, 5 ]
	
	foo(1);
	// 结果:
	// a = 1
	// b = undefined
	// Array []


rest参数只能写在最后，前面用...标识，从运行结果可知，传入的参数先绑定a、b，多余的参数以数组形式交给变量rest，所以，不再需要arguments我们就获取了全部参数。

如果传入的参数连正常定义的参数都没填满，也不要紧，rest参数会接收一个空数组（注意不是undefined）。

因为rest参数是ES6新标准，所以你需要测试一下浏览器是否支持。请用rest参数编写一个sum()函数，接收任意个参数并返回它们的和：


	function foo(){
	   return {name:"foo"};
	}
	foo() //Object {name: "foo"}
	
	function foo(){
	
	  return 
	     {name:"foo"};
	}
	foo() //undefined
	
	function foo(){
	   return {
	    name:"foo"
	};
	
	}
	foo() //Object {name: "foo"}
