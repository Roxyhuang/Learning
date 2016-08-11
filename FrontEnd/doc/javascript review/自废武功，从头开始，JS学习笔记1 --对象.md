自废武功，从头开始，JS学习笔记1 --对象
--
> 本笔记主要是学习http://www.liaoxuefeng.com/wiki/001434446689867b27157e896e74d51a89c25cc8b43bdb3000的笔记

**一、对象**

JavaScript的对象是一种无序的集合数据类型，它由若干键值对组成。

1.对象的定义

	var xiaoming  = {
	    name: '小明',  //是xiaoming的属性
	    birth: 1990,
	    school: 'No.1 Middle School',
	    height: 1.70,
	    weight: 65,
	    score: null
	};

2.对象属性的调用
	
	xiaoming.name; // '小明'
	xiaoming.birth; // 1990

**访问属性是通过.操作符完成的，但这要求属性名必须是一个有效的变量名。如果属性名包含特殊字符，就必须用''括起来：**

	var xiaohong = {
	    name: '小红',
	    'middle-school': 'No.1 Middle School'
	};
	
	xiaohong['middle-school']; // 'No.1 Middle School'
	xiaohong['name']; // '小红'
	xiaohong.name; // '小红'




实际上JavaScript对象的所有属性都是字符串，不过属性对应的值可以是任意数据类型。

如果访问一个不存在的属性会返回什么呢？JavaScript规定，访问不存在的属性不报错，而是返回undefined：

	var xiaoming = {
	    name: '小明'
	};

	xiaoming.age; // undefined

3.添加、删除对象属性

	var xiaoming = {
	    name: '小明'
	};
	xiaoming.age; // undefined
	xiaoming.age = 18; // 新增一个age属性
	xiaoming.age; // 18
	delete xiaoming.age; // 删除age属性
	xiaoming.age; // undefined
	delete xiaoming['name']; // 删除name属性
	xiaoming.name; // undefined
	delete xiaoming.school; // 删除一个不存在的school属性也不会报错




4.检测对象是否拥有某一属性： in操作符 and hasOwnProperty()方法 

实例：

	var xiaoming = {
	    name: '小明',
	    birth: 1990,
	    school: 'No.1 Middle School',
	    height: 1.70,
	    weight: 65,
	    score: null
	};
	'name' in xiaoming; // true
	'grade' in xiaoming; // false



不过要小心，如果in判断一个属性存在，这个属性不一定是xiaoming的，它可能是xiaoming继承得到的：

实例：

	'toString' in xiaoming; // true



要判断一个属性是否是xiaoming自身拥有的，而不是继承得到的，可以用hasOwnProperty()方法：


	var xiaoming = {
	    name: '小明'
	};
	xiaoming.hasOwnProperty('name'); // true
	xiaoming.hasOwnProperty('toString'); // false