自废武功，从头开始，JS学习笔记3--Map和Set
--

**一、ES6的Map：**

　　JavaScript的默认对象表示方式{}可以视为其他语言中的Map或Dictionary的数据结构，即一组键值对。

　　但是JavaScript的对象有个小问题，就是键必须是字符串。但实际上Number或者其他数据类型作为键也是非常合理的。

(1)Map是什么

Map是一组键值对的结构，具有极快的查找速度。

	var names = ['Michael', 'Bob', 'Tracy'];
	var scores = [95, 75, 85];

　　给定一个名字，要查找对应的成绩，就先要在names中找到对应的位置，再从scores取出对应的成绩，Array越长，耗时越长。

　　如果用Map实现，只需要一个“名字”-“成绩”的对照表，直接根据名字查找成绩，无论这个表有多大，查找速度都不会变慢。用JavaScript写一个Map如下：


(2)初始化：

初始化Map需要一个二维数组，或者直接初始化一个空Map。Map具有以下方法：

a.二维数组：

	var m = new Map([['Michael', 95], ['Bob', 75], ['Tracy', 85]]);
	m.get('Michael'); // 95

b.	初始化一个空map

	var m = new Map(); // 空Map
	m.set('Adam', 67); // 添加新的key-value
	m.set('Bob', 59);
	m.has('Adam'); // 是否存在key 'Adam': true
	m.get('Adam'); // 67
	m.delete('Adam'); // 删除key 'Adam'
	m.get('Adam'); // undefined


由于一个key只能对应一个value，所以，多次对一个key放入value，后面的值会把前面的值冲掉：

	
	var m = new Map();
	m.set('Adam', 67);
	m.set('Adam', 88);
	m.get('Adam'); // 88


**二、Set**


Set和Map类似，也是一组key的集合，但不存储呢value。由于key不能重复，在set中，没有重复的key （可以看做，不重复的数组）。
	
	//创建set
	var s1 = new Set();
	
	var s2 = new Set([1,2,3,4,5,6]); //Set {1, 2, 3, 4, 6}
	//重复元素在Set中自动被过滤：
	var s3 - new Set([1,2,3,4,5,6,6,6])  Set {1, 2, 3, 4, 6}


通过add(key)方法可以添加元素到Set中，可以重复添加，但不会有效果：

	var vs = new Set([1,2])  //Set {1, 2}
	vs.add(3)
	Set {1, 2, 3}


通过delete(key)方法可以删除元素：

	var vs = new Set([1,2])  //Set {1, 2}
	vs.add(3)
	vs.delete(3) //Set {1, 2}


**三、iterable**


**(1) for...of循环**
	
遍历Array可以采用下标循环，遍历Map和Set就无法使用下标。为了统一集合类型，ES6标准引入了新的iterable类型，Array、Map和Set都属于iterable类型。

具有iterable类型的集合可以通过新的for ... of循环来遍历。
for ... of循环是ES6引入的新的语法，请测试你的浏览器是否支持：


	var a = ['a','b','c'];
	
	var b = new Map([[1,'a'],[2,'b'],[3,'c']]);
	
	var c = new Set(['a','b','c']);
	

	//数组
	for (var i of a){
	
	  console.log(i); //a b c
	
	}
	
	//Map
	for (var i of b){
	
	  console.log(i);  //[1, "a"] [2, "b"] [3, "c"]
	
	}

	//Set
	for (var i of c){
	
	  console.log(i); //a b c
	
	}


**（2）for ... of 和 for ... in 的区别**

for ... in循环将把name包括在内，但Array的length属性却不包括在内。

for ... of循环则完全修复了这些问题，它只循环集合本身的元素：




	
	var a =['A','B','C'];
	a.name="123"; 

	// for ... in 
	for(let i in a){
	
	   console.log(i); // "A" "B" "C" "123"
	}

	// for ... of 
	for (let i of a){
	
	  console.log(i); // "A" "B" "C"
	
	}


**(3) forEach() 循环 （es 5.1引入)**

　　然而，更好的方式是直接使用iterable内置的forEach方法，它接收一个函数，每次迭代就自动回调该函数。
	
Array:

    var a = ["a","b","c"];

	a.forEach(function(element,index,array){
	
	  console.log(element); // "a" "b" "c"
	  console.log(index);   // 0 1 2
	  console.log(array);   //["a", "b", "c"] *3
	
	});

Set:
Set与Array类似，但Set没有索引，因此回调函数的前两个参数都是元素本身

	var s = new Set(["a","b","c"]);

	s.forEach(function(element,sameElement,set){
	console.log(element); // "a" "b" "c"
	console.log(sameElement);  // "a" "b" "c"
	console.log(set); //Set {"a", "b", "c"}
	});

Map:

Map的回调函数参数依次为value、key和map本身：


	var m = new Map([[1,'x'],[2,'y'],[3,'z']]);
	
	m.forEach(function(value,key,map){
	   console.log(value);  //x y z
	   console.log(key);    // 1 2 3
	   console.log(map);    //Map {1 => "x", 2 => "y", 3 => "z"}
	
	})

如果对某些参数不感兴趣，由于JavaScript的函数调用不要求参数必须一致，因此可以忽略它们。例如，只需要获得Array的element：