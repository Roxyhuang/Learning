前端通过面试题来提高--CSS篇
--
> 引用
> https://github.com/markyun/My-blog/blob/master/Front-end-Developer-Questions/Questions-and-Answers/README.md


**1.介绍一下标准的CSS的盒子模型？低版本IE的盒子模型有什么不同的？**
   
	(1) IE盒子模型，w3c盒子模型
		   
	(2) 盒子模型：content padding border margin

	(3) ie与w3c盒子模型不同之处是 ie的content将padding和border同算进去了


**2.CSS选择符有哪些，哪些属性可以被继承？**

	（1）id选择器 	//#class
	（2）类选择器 	//.class
	（3）标签选择器	//div,h1,p
	（4）后代选择器   //classA classB
	（5）相邻选择器   //classA + classB
	（6) 属性选择器   //[name="A"]
	 (7) 伪劣选择器   a:last
	 (8) 子选择器     classA > classB
     (9) 通配符选择器  *

	 可继承样式：font-size;color;font-family;UL;LI;DL;DD;DT;

     不可继承样式：boder;padding;margin;width;height;

**3.CSS优先级算法如何计算？**

	(1)优先级就近原则，同权重情况样式定义最近者为准；

    (2)载入样式最后载入的定位为准；

优先级：

	!important > id > class > tag

    important 比内联样式优先级高		



**4.CSS3新增伪类有那些？**

举例：

 p:first-of-type 选择属于父元素的首个<p>元素的每个<p>元素

 p:last-of-type  选择属于其父元素的最后 <p> 元素的每个 <p> 元素。

 p:only-of-type  选择属于其父元素唯一的 <p> 元素的每个 <p> 元素。

