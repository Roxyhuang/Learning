自废武功，从头开始，JS学习笔记6 --方法
--

**一、方法**

在一个对象中绑定函数，称为这个对象的方法。


	var xiaoming = {
	    name: '小明',
	    birth: 1990,
	    age: function () {
	        var y = new Date().getFullYear();
	        return y - this.birth;
	    }
	};
	
	xiaoming.age; // function xiaoming.age()
	xiaoming.age(); // 今年调用是25,明年调用就变成26了


绑定到对象上的函数称为方法，和普通函数也没啥区别，但是它在内部使用了一个this关键字，这个东东是什么？

在一个方法内部，this是一个特殊变量，它始终指向当前对象，也就是xiaoming这个变量。所以，this.birth可以拿到xiaoming的birth属性。

让我们拆开写：


function getAge() {
    var y = new Date().getFullYear();
    return y - this.birth;
}

var xiaoming = {
    name: '小明',
    birth: 1990,
    age: getAge
};

xiaoming.age(); // 25, 正常结果
getAge(); // NaN


修复的办法也不是没有，我们用一个that变量首先捕获this：

	'use strict';
	
	var xiaoming = {
	    name: '小明',
	    birth: 1990,
	    age: function () {
	        var that = this; // 在方法内部一开始就捕获this
	        function getAgeFromBirth() {
	            var y = new Date().getFullYear();
	            return y - that.birth; // 用that而不是this
	        }
	        return getAgeFromBirth();
	    }
	};

xiaoming.age(); // 25
用var that = this;，你就可以放心地在方法内部定义其他函数，而不是把所有语句都堆到一个方法中。

**二、this指向问题**
 

指向另一篇

   





**三、apply函数**

　　虽然在一个独立的函数调用中，根据是否是strict模式，this指向undefined或window，不过，我们还是可以控制this的指向的！