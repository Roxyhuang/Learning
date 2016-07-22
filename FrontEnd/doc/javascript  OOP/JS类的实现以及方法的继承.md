我常用的JS继承和类的写法
--
> 引用自http://www.cnblogs.com/dolphinX/p/4381855.html


**JS通常类的实现：**

	//代码片段
	function  people(name,age,sex,type){
	    this.name = name;
	    this.age = age;
	    this.sex = sex;
	    this.type = type;
	}
	people.prototype.say = function(){
	    document.write("我是没有职业的人");
	}
	
	var work = new people("小李",23,"男","工人");
	work.say = function(){
	    document.write(this.name + this.age);
	}
	work.say();//输出了 小李23
	
	
	var student = new people("阿张",25)
	student.say();//我是没有职业的人


**js混合继承：**
	
	//代码片段
	function parent(name,type) {
	    this.name = name;
	    this.type = type;
	}
	parent.prototype.hello = function(){
	    console.log(this.name + this.type);
	}
	
	function chlid(name,type){
	    parent.apply(this,arguments);
	}
	chlid.prototype =new parent();
	
	var boy = new chlid("一拳","超人");
	
	console.log(boy.name);
	boy.hello();
