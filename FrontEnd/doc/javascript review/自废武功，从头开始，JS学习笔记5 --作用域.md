自废武功，从头开始，JS学习笔记5 --变量作用域
--

在JavaScript中，用var申明的变量实际上是有作用域的。

**一、如果一个变量在函数体内部申明，则该变量的作用域为整个函数体，在函数体外不可引用该变量：**

'use strict';

function foo() {
    var x = 1;
    x = x + 1;
}

x = x + 2; // ReferenceError! 无法在函数体外引用变量x


**二、如果两个不同的函数各自申明了同一个变量，那么该变量只在各自的函数体内起作用。换句话说，不同函数内部的同名变量互相独立，互不影响：**	


	'use strict';
	
	function foo() {
	    var x = 1;
	    x = x + 1;
	}
	
	function bar() {
	    var x = 'A';
	    x = x + 'B';
	}




**三、由于JavaScript的函数可以嵌套，此时，内部函数可以访问外部函数定义的变量，反过来则不行：**


'use strict';

function foo() {
    var x = 1;
    function bar() {
        var y = x + 1; // bar可以访问foo的变量x!
    }
    var z = y + 1; // ReferenceError! foo不可以访问bar的变量y!
}