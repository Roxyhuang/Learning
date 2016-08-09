为什么要使用Base64？以及atob方法和btoa方法
--

> http://www.codeweblog.com/javascript-%E4%BD%BF%E7%94%A8btoa%E5%92%8Catob%E6%9D%A5%E8%BF%9B%E8%A1%8Cbase64%E8%BD%AC%E7%A0%81%E5%92%8C%E8%A7%A3%E7%A0%81/

**Base64是什么：**

　　Base64是网络上最常见的用于传输8Bit字节代码的编码方式之一Base64主要用于将不可打印的字符转换成可打印字符，或者简单的说将二进制数据编码成ASCII字符。

　　将二进制数据编码成ASCII字符主要的目的是能在纯文本内容中插入二进制数据，常见的应用场景包括：
	
1.电子邮件

2.微软的MHT格式

3.XML文件

4.DATA URL

(1)传输信道只支持ASCII字符，不方便传输二进制流的场合。

(2)含有非ASCII字符，容易出现编码问题的场合。

(3)简易的掩人耳目。至少非开发人一眼看不出来是啥。



**无汉字转换:**

	var str =`js.js.js.oh!yeah`;
	var b = window.atob(str);	//"ÈìÈìË#¢j"
	var str = `jsjsjsjsjssjohyeah`;
	var b = window.atob(str);
	var c = window.btoa(b); "jsjsjsjsjssjohyeag=="



**汉字转换：**

	var str = `china,中国`
	
	window.btoa(window.encodeURIComponent(str))；

	//"Y2hpbmElMkMlRTQlQjglQUQlRTUlOUIlQkQ="；

	var a = window.btoa(window.encodeURIComponent(str))；

	window.decodeURIComponent(window.atob(a));
	//"china,中国"