JS this关键字的一些解析学习笔记
--

>引用自 http://www.ibm.com/developerworks/cn/web/1207_wangqf_jsthis/


**一、js中this含义的定义浅析**


**java等面向对向语言中：**this关键字的含义是明确具体的，即指代当前对向，一般在编译期确定下来，或称为编译期绑定

**js：**而在 JavaScript 中，this 是动态绑定，或称为运行期绑定的，这就导致 JavaScript 中的 this 关键字有能力具备多重含义，带来灵活性的同时，也为初学者带来不少困惑。

**二、Java 语言中的 this：**

在 Java 中定义类经常会使用 this 关键字，多数情况下是为了避免命名冲突，比如在下面例子的中，定义一个 Point 类，很自然的，大家会使用 x，y 为其属性或成员变量命名，在构造函数中，使用 x，y 为参数命名，相比其他的名字，比如 a，b，也更有意义。这时候就需要使用 this 来避免命名上的冲突。另一种情况是为了方便的调用其他构造函数，比如定义在 x 轴上的点，其 x 值默认为 0，使用时只要提供 y 值就可以了，我们可以为此定义一个只需传入一个参数的构造函数。无论哪种情况，this 的含义是一样的，均指当前对象。


	public class Point { 
	    private int x = 0; 
	    private int y = 0; 
	    
	    public Point(x, y){ 
	        this.x = x; 
	        this.y = y; 
	    } 
	    
	    public Point(y){ 
	        this(0, y); 
	    } 
	 }


**三、JavaScript 语言中的 this：**

由于其运行期绑定的特性，JavaScript 中的 this 含义要丰富得多，它可以是全局对象、当前对象或者任意对象，**这完全取决于函数的调用方式。**

**（1）作为对象方法调用：**

在 JavaScript 中，函数也是对象，因此函数可以作为一个对象的属性，此时该函数被称为该对象的方法，在使用这种调用方式时，this 被自然绑定到该对象。

	 var point = { 
	 x : 0, 
	 y : 0, 
	 moveTo : function(x, y) { 
	     this.x = this.x + x; 
	     this.y = this.y + y; 
	     } 
	 }; 
	
	 point.moveTo(1, 1)//this 绑定到当前对象，即 point 对象

**（2）作为函数调用**

函数也可以直接被调用，此时 this 绑定到全局对象。在浏览器中，window 就是该全局对象。比如下面的例子：函数被调用时，this 被绑定到全局对象，接下来执行赋值语句，相当于隐式的声明了一个全局变量，这显然不是调用者希望的。


 function makeNoSense(x) { 
 this.x = x; 
 } 

 makeNoSense(5); 
 x;// x 已经成为一个值为 5 的全局变量


**（3）作为构造函数调用**

JavaScript 支持面向对象式编程，与主流的面向对象式编程语言不同，JavaScript 并没有类（class）的概念，而是使用基于原型（prototype）的继承方式。相应的，JavaScript 中的构造函数也很特殊，如果不使用 new 调用，则和普通函数一样。作为又一项约定俗成的准则，构造函数以大写字母开头，提醒调用者使用正确的方式调用。如果调用正确，this 绑定到新创建的对象上。