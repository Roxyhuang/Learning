js的浅拷贝和深拷贝
--
> 参考：http://www.jianshu.com/p/afc55e33a36a

有一天一个哥们给我看了一套面试题，当时我和这个博主一样，觉得碉堡了，什么web现在开始玩克隆技术了？ 想想不可能啊？咱们只是纯虚拟资产啊，恰好学习时看到这一篇文章，


**知乎上有一句话是这样的：**

> 什么叫做理解了某一个概念？就是你可以用简单的语言把这个概念对你六岁的小侄女讲明白。


**1.深拷贝的概念**

深度克隆就是：把一个对象里面的东西一模一样地复制到另一个对象，并且这两个对象分别放在内存的不同地方。

	
	
	let userTemplate = {
	    name:"名字",
	    tag:["帅哥","碉堡了"],
	    username:"admin",
	    password:"12345678"
	}
	
	//浅克隆
	const extendCopy = obj=> {
	    let newObj = {};
	    for( let i in  obj ){
	        newObj[i] = obj[i];
	    }
	    return newObj
	};

	//深克隆
	
		function extendDeepCopy(obj,newObj){
	    var newObj = newObj || {};
	    for (var i in obj ){
	        if(typeof  obj[i] =="object"){
	            newObj[i] = (obj[i].constructor===Array)?[]:{};
	            extendDeepCopy(obj[i],newObj[i]);
	        }else{
	            newObj[i] = obj[i];
	        }
	        return newObj;
	    }
	}


	
	let user =extendCopy(userTemplate);
	user.name = "小哥";
	user.username = "admin123";
	user.password = "23456789";
	user.tag.push("小帅哥");
	
	
	let user2 = extendCopy(userTemplate);
	user2.name = "小美女";
	user2.username ="admin456";
	user2.password = "34567890";
	user2.tag.push("牛")
	
	
	console.log(user);　
	console.log(user2);


结果傻逼了，数组属性出现了问题，2个对象的数组属性都一样。
因为简单的复制对象，如果对象其中一个属性是引用型变量，就会出现这种情况，因为引用型变量保存的是内存地址，所以其实后来操作的都是同一块内存，导致了数组内容都一样。  这就是浅克隆了。

array:concat()

Jq:$.extend()

es6: Object.assign()




