JavaScript OOP开发 面向对象
--
> 本文参考：http://www.hubwiz.com/class/574bac8cda97b6e9299d2f04

**面向对象：**  

　　　　JavaScript在设计之初就是一种面向对象的语言，虽然我们在日常的开发中很少能体验到这一点。面向对象语言往往有个特征就是需要new一个实例。而JavaScript也确实如此：

	 var dNow = new Date();
     var obj = new Object();

面向对象拥有三大特征  
1.封装  
2.继承  
2.多态  

**基于原型：** 

　　JavaScript是一款基于原型模式的面向对象语言。

　　我们可以把原型理解为是一个使用说明书，每一个类型都会有一个对应的使用说明书，凡是使用说明上规定的成员，都是可以使用的。

　　比如电视器的说明书上规定了开机、关机、换台等行为，那么每一台电视机都会具备这些功能。

　　并且我们还可以通过JavaScript代码为指定的类型的使用说明添加新的成员。 



**原始对象：**

 　　我们都知道面向对象中最重要的环节是封装。JavaScript提供了定义一个原始对象的方法，详细代码请见下面的示例：



        var worker = new Object();
        worker.isWorking = false;        //通过明确的属性名添加成员

        var str = "phone";
        worker[str] = 13800000000;    //通过不明确的属性名添加成员（str可变，因此不明确）

        var phone = worker.phone;    //通过不明确添加的成员，可以进行明确的访问；也可以通过不明确的方式访问明确的成员。
        var name = worker["name"]; 


　　示例中我们发现，通过构建一个Object实例，我们可以为该实例手动添加任何成员，可以是字符、数字、布尔甚至于一个方法，定义的方式，即可以用实例名.成员名 = 内容，也可以使用实例名["成员名"] = 内容。



当然目前我更常用的方式是这样的：

	 var worker = {
	        name : "John",
	        age : 30,
	        isWorking : false,
	        startWork : function(){
	            if(!this.isWorking){
	                this.isWorking = true;
	            }
	        }
	    };


　　通过上面的方法，我们可以定义一个对象，将对象上的属性定义后便完成了封装的工作。之后，我们只需要调用对象上的成员，就可以相应的操作了。


**原始对象的封装**
	 
　　不难发现的一点是，通过上面的方法定义的对象，缺少了复用性。也就是说，我们每次都要写name、age、isWorking等等等等，才能创建一个新的对象实例，这肯定是不合理的。

	function newHuman(name, age){
	return {
    	name : name,
        age : age,
        sayHello : function(){
        	document.write("Hello World! I'm " + this.name);
        }
    };
	};
	
	var h = newHuman("Neo",25);
	h.sayHello();

通过一个function的封装，我们可以每次获得一个相同结构的实例。　　


**构造函数：**

　　上节中的newWorker并不是真正的构造函数，JavaScript中提供了真正的构造函数，它的语法和定义一个function其实是一样的：


    function people(name,age){
            this.name = name ,
            this.age = age ,
            this.sayHello = function(){
                console.log("HelloWorld"+"我的名字是"+ this.name +"我今年"+this.age +"岁" )
            }
        }
        var tom = new people("tom","22");
        var jack = new people("jack","29");
        tom.sayHello();
        jack.sayHello();

		document.write(tom.sayHello == jack.sayHello);


　　另外通过右边的例子，我们还可以发现jim和tom的startWork并不指向不一个内存，也就意味着，当我们有很多实例的时候，内存开销会非常大。

**继承**

　　继承的核心其实就是拥有自己的定义的成员，也拥有父类型的成员
我们先从jquery提供的继承方法开始说


　　JQuery提供了对原始对象的简单继承方法：$.extend，它会使用后面的对象与前面的对象的成员加起来，成生新的对象。

	