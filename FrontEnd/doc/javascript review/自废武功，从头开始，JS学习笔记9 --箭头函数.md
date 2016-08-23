自废武功，从头开始，JS学习笔记9 --箭头函数
--
**
一、箭头函数**

ES6标准新增了一种新的函数：Arrow Function（箭头函数）。为什么叫Arrow Function？因为它的定义用的就是一个箭头：


	x => x * x

上面的箭头函数相当于：

	function (x) {
	    return x * x;
	}


箭头函数相当于匿名函数，并且简化了函数定义。箭头函数有两种格式，一种像上面的，只包含一个表达式，连{ ... }和return都省略掉了。**还有一种可以包含多条语句，这时候就不能省略{ ... }和return：**

	
	x => {
	    if (x > 0) {
	        return x * x;
	    }
	    else {
	        return - x * x;
	    }
	}

如果参数不是一个，就需要用括号()括起来：


  //两个参数

	var fn = (x,y) =>  x*x + y*y;

  //无参数

    var hey = () => "helloWorld"

  //可变参数

	var fn2 = (x,y, ...rest) =>{
	     let sum = x + y;
	     for(let i=0 ; i<rest.length;i++){
	       sum +=rest[i];
	     }
	     return sum;
	}

**二、this：**


箭头函数看上去是匿名函数的一种简写，但实际上，箭头函数和匿名函数有个明显的区别：箭头函数内部的this是词法作用域，由上下文确定。

回顾前面的例子，由于JavaScript函数对this绑定的错误处理，下面的例子无法得到预期结果：



	var obj = {
	    birth: 1990,
	    getAge: function () {
	        var b = this.birth; // 1990
	        var fn = function () {
	            return new Date().getFullYear() - this.birth; // this指向window或undefined
	        };
	        return fn();
	    }
	};


现在，箭头函数完全修复了this的指向，this总是指向词法作用域，也就是外层调用者obj：

	var obj = {
	    birth: 1990,
	    getAge: function () {
	        var b = this.birth; // 1990
	        var fn = () => new Date().getFullYear() - this.birth; // this指向obj对象
	        return fn();
	    }
	};
	obj.getAge(); // 25


如果使用箭头函数，以前的那种hack写法：

	var that = this;

就不再需要了。

由于this在箭头函数中已经按照词法作用域绑定了，所以，用call()或者apply()调用箭头函数时，无法对this进行绑定，即传入的第一个参数被忽略：

	var obj = {
	    birth: 1990,
	    getAge: function (year) {
	        var b = this.birth; // 1990
	        var fn = (y) => y - this.birth; // this.birth仍是1990
	        return fn.call({birth:2000}, year);
	    }
	};
	obj.getAge(2015); // 25