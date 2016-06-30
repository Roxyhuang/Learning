JavaScript OOP开发 继承
--
> 本文参考：http://www.hubwiz.com/class/574bac8cda97b6e9299d2f04


**JS继承方式**  
	
　　　继承的核心其实就是拥有自己的定义的成员，也拥有父类型的成员

　　　和其他功能一样，JS实现继承的方式不止一种。这是因为 JavaScript 中的继承机制并不是明确规定的，而是通过模仿实现的。这意味着所有的继承细节并非完全由解释程序处理。作为开发者，你有权决定最适用的继承方式。
 
**下面为具体的继承方式可总结为：**  
1. 对象冒充:  

(1) 原生JS形式的对象冒充  
(2) call() 方法   
(3) apply() 方法  

2.原型链（prototype chaining):

3.混合方式
  
*.  jQuery提供的$.extend方法

目前我比较常用的就是这几种，jQuery的我们也会分析一下。
	


***jQuery提供的继承方法**

　　
我们先从jquery提供的继承方法开始说


　　JQuery提供了对原始对象的简单继承方法：$.extend，它会使用后面的对象与前面的对象的成员加起来，成生新的对象。（他的核心原理是合并对象）

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

**1.对象冒充**

**父类型的构造函数**

　　由于父类型的构造函数是由function创建的类型，其自身无法使用&.extend进行继承的。就像Java、C#等语言一样，继承时，子类必须在构造函数时调用父类型的构造函数。JavaScript实现类继承的第一步便是调用父类型的构造函数。


















		function leader(name,age){
		    worker.apply(this,arguments);
		}

上述代码就已经完成了对父类型构造函数的调用，这里我来详细解释一下：

1、apply这是JavaScript内置的一个方法，只要是声明成为function的对象，都会拥有该成员。对于后台技术较高的同学，你可以将apply理解为反射调用。对于并不了解反射的同学，可以这样理解：我们正常情况下调用一个方法是对象.方法名(参数列表)，使用apply的话，我们就是方法名.apply(对象，参数列表)，顺序不一样了

2、arguments这个关键字只能在function内部使用，表示的是参数列表，在上述示例中arguments中包含的就是name和age。

3、通过worker.apply(this,arguments)，相当于使用当前实例和当前参数列表执行了一次worker方法，也就意味着将当前实例和name，age进行了一次worker的构造。


http://blog.csdn.net/business122/article/details/8000676


http://www.w3school.com.cn/js/pro_js_syntax.asp