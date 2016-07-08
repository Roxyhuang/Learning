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














最近最网上看了一个人面试淘宝时的经历，然后发现了自己有好多好多不太清楚的地方，所以特此写点文章来加深自己对一些问题的理解。
文章中提到了一个问题是：JavaScript是如何实现继承的？

下面我便阐述一些在网上找到的方法和实例来解释下，借以加深自己的印象。
我们知道JavaScript中的function是万能的，除了用于的函数定义，也可以用于类的定义。
JavaScript的继承，说起来也是有点怪，不像C++和一些面向对象的语言，他没有public,private等访问控制修饰，也没有implement或其他特定的符号来说明是实现继承。
关于javascript类的继承可以参考一下下面的这个例子。
复制代码 代码如下:

<script type="text/javascript"> 
function Person() {
    // 属性 
    this.Gender = "female";
    this.Age = 18;
    this.Words = "Silence";
    // 方法
    this.shouting = function() {
        alert("开心哦！父类的方法");
    }
}
// 继承
function Programmer() {
    this.base = Person;
}
Programmer.prototype = new Person;
// 为子类添加新的方法
Programmer.prototype.typeCode = function() {
    alert("俺是敲代码的！IT民工，很不开心。子类的方法");
}
// 调用示例
function sayHello() {
    var a = new Programmer();
    alert(a.Gender); // 调用父类的属性
    a.shouting(); // 调用父类的方法
    a.typeCode(); // 调用子类的方法
}        
sayHello();
</script>
上例中，首先是声明一个person类，里面包含了一些属性和方法，然后接着又声明了一个programmer类，其中有个base属性，这个属性并不是必需的，但是出于规范以及以后在查找对象所继承的类时都需要写上，然后是给programmer的原型对象（prototype）拷贝了person类；于是便实现了类的继承。
模拟JavaScript中类和继承的一些原理
在面向对象的语言中，我们使用类来创建一个自定义对象。然而JavaScript中所有事物都是对象，那么用什么办法来创建自定义对象呢？
这就需要引入另外一个概念 - 原型（prototype），我们可以简单的把prototype看做是一个模版，新创建的自定义对象都是这个模版（prototype）的一个拷贝 （实际上不是拷贝而是链接，只不过这种链接是不可见，给人们的感觉好像是拷贝）。
让我们看一下通过prototype创建自定义对象的一个例子：
复制代码 代码如下:

// 构造函数
  function Person(name, sex) {
      this.name = name;
      this.sex = sex;
  }
  // 定义Person的原型，原型中的属性可以被自定义对象引用
  Person.prototype = {
      getName: function() {
          return this.name;
      },
      getSex: function() {
          return this.sex;
      }
  }
这里我们把函数Person称为构造函数，也就是创建自定义对象的函数。可以看出，JavaScript通过构造函数和原型的方式模拟实现了类的功能。
下面通过一个例子来具体阐述创建一个自定义对象，javascript所做的具体的工作：
复制代码 代码如下:

var zhang = new Person("ZhangSan", "man");
console.log(zhang.getName()); // "ZhangSan"
var chun = new Person("ChunHua", "woman");
console.log(chun.getName()); // "ChunHua"
当代码var zhang = new Person("ZhangSan", "man")执行时，其实内部做了如下几件事情：
创建一个空白对象（new Object()）。
拷贝Person.prototype中的属性（键值对）到这个空对象中（我们前面提到，内部实现时不是拷贝而是一个隐藏的链接）。
将这个对象通过this关键字传递到构造函数中并执行构造函数。
将这个对象赋值给变量zhang。
所有工作完成。
为了证明prototype模版并不是被拷贝到实例化的对象中，而是一种链接的方式，请看如下代码：
复制代码 代码如下:

function Person(name, sex) {
    this.name = name;
    this.sex = sex;
}
Person.prototype.age = 20;
var zhang = new Person("ZhangSan", "man");
console.log(zhang.age); // 20
// 覆盖prototype中的age属性
zhang.age = 19;
console.log(zhang.age); // 19
delete zhang.age;
// 在删除实例属性age后，此属性值又从prototype中获取
console.log(zhang.age); // 20
在上面的这个例子中，如果他仅仅是通过拷贝得来的，则在删除了这个age这个属性后，这个对象里面将不会存在，但是例子中的age属性还能输出，还是覆盖以前的值，说明我们仅仅是删除了子类中同名的属性，而父类当中的age属性通过一种不可见的链接依然存在在对象中。
如何在JavaScript中实现简单的继承？
下面的例子将创建一个雇员类Employee，它从Person继承了原型prototype中的所有属性。
复制代码 代码如下:

function Employee(name, sex, employeeID) {
    this.name = name;
    this.sex = sex;
    this.employeeID = employeeID;
}
// 将Employee的原型指向Person的一个实例
// 因为Person的实例可以调用Person原型中的方法, 所以Employee的实例也可以调用Person原型中的所有属性。
Employee.prototype = new Person();
Employee.prototype.getEmployeeID = function() {
    return this.employeeID;
};
var zhang = new Employee("ZhangSan", "man", "1234");
console.log(zhang.getName()); // "ZhangSan

好了，以上就是一些关于javascript实现继承的具体过程，和实现继承的方法。
当然总结一下，javascript中的继承机制仅仅是靠模拟的，于一些面向对象的语言来讲，显的粗糙而且还有一些缺陷，不过总的来讲，这依然不并会降低前端开发者在这方面的热情。