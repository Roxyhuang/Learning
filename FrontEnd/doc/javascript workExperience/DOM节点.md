DOM节点讲解
---

**一、DOM是什么：**
DOM（文档对象模型）是针对HTML和XML文档的一个API，通过DOM可以去改变文档。


　　简而言之，DOM可以理解为一个访问或操作HTML各种标签的实现标准。
对于一个HTML来说，文档节点Document（看不到的）是它的根节点，对应的对象便是document对象（严格讲是子类HTMLDocument对象，下面单独介绍Document类型时会指出）。
换句话说存在一个文档节点Document，然后它有子节点，比如通过document.getElementsByTagName(“html”)，得到类型为元素节点的Element html。

**二、Node类型（基类，所有节点都继承了它的方法）**
先讲Node类型的属性
首先是nodeType属性，用来表明节点类型的，例如：
　　　　　

	document.nodeType;
	// 返回 9 ，其中document对象为文档节点Document的实例
		
		元素类型    节点类型
		  元素          1
		  属性          2
		  文本          3
		  注释          8
		  文档          9


