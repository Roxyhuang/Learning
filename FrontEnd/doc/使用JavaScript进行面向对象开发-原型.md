JavaScript OOP开发 原型与继承
--
> 本文参考：http://www.hubwiz.com/class/574bac8cda97b6e9299d2f04

**原型：**

   　　仅仅通过构造函数创建实例，他们的成员并不共用，很明显这不是一个好的实现方法。  

　　这一节我们向你隆重的介绍prototype这个概念，它便是原型。任何类型都会有属于自己的原型，并且原型上定义的成员，可以在每个实例中引用，并且是共用的。我们可以先看看下面的运行结果。

　　结果很明显，这次两个不同实例的startWork是相同的了，这意味着不同实例间共用了该方法。

　　那么在设计JavaScript面向对象类型的时候，我们一般遵循以下规则：


　　因为实例不同而不同的内容，用this关键字声明
无论实例怎样内容完全相同的成员，定义在prototype上


**扩展已知原型：**

　　我们不难发现，JavaScript原型定义成员的方法和我们平时使用Java、C#、VB等语法结构不同。大部分语言是要将成员定义写在类型定义域内部的，而JavaScript是写在外部的。

	function worker(name,age){
	    //some code here
	} //类型定义结束
	 
	worker.prototype.startWork = function(){
	    //some code here
	};

　　这种特殊的语法结构允许我们可以扩展和修改已有的类型，比如*String*，*Date*等。 比如，根据浏览器不同，不是所有JavaScript中的String都支持startWith这样的方法，那么我们可以自己实现一个

	String.prototype.startWith = function(str){
    return this.indexOf(str) == 0;
};
 
	var str = "Hello World!";
	document.write(str.startWith("Hello"));        //true

**继承**

　　继承的核心其实就是拥有自己的定义的成员，也拥有父类型的成员
我们先从jquery提供的继承方法开始说


　　JQuery提供了对原始对象的简单继承方法：$.extend，它会使用后面的对象与前面的对象的成员加起来，成生新的对象。

	//定义一个工人
    var worker = {
        name : "",
        age : 0,
        isWorking : false,
        startWork : function(){
            //some code here
        }
    };
 
    //定义一个工头，工头本身也是工人，但他有一个额外的属性，用于记录他所管理的员工列表，并且可以指挥一名工人开工
    var leader = $.extend(worker,{
        workers : [],
        callStart : function(worker){
            //指挥一名工人开工
        }
    });
 
    //此时的leader除了拥有name，age，isWorking，startWork这四项属性之外，还拥有workers和callStart成员。
 
*$.extend$还可以重写对象上的成员

    var worker = {
        position : "worker" //职位
    };
    var leader = $.extend(worker,{
        position : "leader"
    });
 
    document.write(leader.position);        //leader