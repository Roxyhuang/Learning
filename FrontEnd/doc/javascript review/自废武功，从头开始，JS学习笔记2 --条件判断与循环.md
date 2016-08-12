自废武功，从头开始，JS学习笔记2 --条件判断与循环
--
> http://www.liaoxuefeng.com/wiki/001434446689867b27157e896e74d51a89c25cc8b43bdb3000/0014345005693811782d9e338994ec19aa1c5325824bc15000


**一、条件判断**

一般项目中我们的写法都是：

	if(){
		...
	}else{
	
	}

但是其实语句块只包含一句的话，可以这么写：

	var ages = 20 ;
	
	if(ages>=10)
	
	    console.log(123);
	else
	    console.log(456);

**省略{}的危险之处在于，如果后来想添加一些语句，却忘了写{}，就改变了if...else...的语义，例如：**

	var age = 20;
	if (age >= 18)
	    alert('adult');
	else
	    console.log('age < 18'); // 添加一行日志
	    alert('teenager'); // <- 这行语句已经不在else的控制范围了

**所以最后else一定要写{}**



**二、多行条件判断**
	
如果还要更细致地判断条件，可以使用多个if...else...的组合：

	var age = 3;
	if (age >= 18) {
	    alert('adult');
	} else if (age >= 6) {
	    alert('teenager');
	} else {
	    alert('kid');
	}
	
请注意，if...else...语句的执行特点是二选一，在多个if...else...语句中，如果某个条件成立，则后续就不再继续判断了。



**三、if的条件判断语句结果不是true或false怎么办？**
实例：

var s = '123';
if (s.length) { // 条件计算结果为3
    //
}

JavaScript把null、undefined、0、NaN和空字符串''视为false，其他值一概视为true，因此上述代码条件判断的结果是true。


实例：


	'use strict';
	
	var height = parseFloat(prompt('请输入身高(m):'));
	var weight = parseFloat(prompt('请输入体重(kg):'));
	var bmi = weight/Math.pow(height,2);
	if(bmi>0 && bmi<18.5){
	
	   alert(`太TM的轻了`);
	
	}else if(bmi>=18.5 && bmi<25){
	    
	   alert(`太TMD正常`);
	}else{
	
	    alert(`太TMD胖了`);
	}



**四、循环**

要计算1+2+3，我们可以直接写表达式：

（1）for循环


实例：

	var x = 0 
	
	for (let i = 0 ;i<100;i++){
	   x = x + i; 
	    
	}
	console.log(x);

for循环最常用的地方是利用索引来遍历数组：

    var arr = ['apple','google','facebook'];
	for (let i  = 0; i<arr.length;i++){
	    console.log(arr[i]);
	}

for循环的3个条件都是可以省略的，如果没有退出循环的判断条件，就必须使用break语句退出循环，否则就是死循环：

	var x = 0;
	for (;;) { // 将无限循环下去
	    if (x > 100) {
	        break; // 通过if判断来退出循环
	    }
	    x ++;
	}

	

（2）for ... in 循环

for循环的一个变体是for ... in循环，它可以把一个对象的所有属性依次循环出来：

	var xiang ={
	    name:"爱香",
	    age:25,
	    live:"11"
	
	}
	
	for (var i in xiang){
	
	  console.log(xiang[i]);
	
	}

要过滤掉对象继承的属性，用hasOwnProperty()来实现：

	
	var xiang ={
	    name:"爱香",
	    age:25,
	    live:"11"
	
	}

	for (var key in xiang){
	   if(xiang.hasOwnProperty(key)){
	   console.log(key); 
	 
	}

	
	for ( i in a){
	  
	  console.log(arr[i]);
	}
	for ( i in a){
	  
	   console.log(a[i]);
	}




（3）while

	由于Array也是对象，而它的每个元素的索引被视为对象的属性，因此，for ... in循环可以直接循环出Array的索引：
	
	var a = ['A', 'B', 'C'];
	for (var i in a) {
	    alert(i); // '0', '1', '2'
	    alert(a[i]); // 'A', 'B', 'C'
	}
	
	请注意，for ... in对Array的循环得到的是String而不是Number。




（4）do ... while循环

最后一种循环是do { ... } while()循环，它和while循环的唯一区别在于，不是在每次循环开始的时候判断条件，而是在每次循环完成的时候判断条件：


	var n = 0;
	do {
	    n = n + 1;
	} while (n < 100);
	n; // 100


用do { ... } while()循环要小心，循环体会至少执行1次，而for和while循环则可能一次都不执行。

