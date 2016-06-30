一、实例化AJAX对象
1、实例化XMLHttpRequest对象：var request=new XMLHttpRequest();
2、浏览器的支持情况：大部分浏览器都支持，但是在IE5/IE6不能支持，但是也可以通过添加代码使得IE5/IE6支持。
兼容IE6函数
var request;
if(window.XMLHttpRequest){
request = new XMLHttpRequest(); //IE7+，Firefox，Chrome，Opera，Safari...
}else{
request = new ActiveXObject("Microsoft.XMLHTTP"); //IE6,IE5
}

二、
XMLHttpRequest发送请求：
两个方法
open(method,url,async)
method：规定HTTP发送请求的方式是get还是post,不区分大小写，一般来说用大写
url：请求地址(相对地址或绝对地址)
async:同步/异步(false/true)，默认是异步也就是true，可以不用填写

send(string):发送到服务器（该参数可以填或者不填-----get方法不填或填null，post:一般要填）

例如：
request.open("POST","create.php",true);
request.setRequestHeader("Content-type","application/x-www-form-urlencoded ")//设置HTTP头信息--一定要写在open()和send()之间
request.send("name=xxxx&set=xxx");




三、
XMLHttpRequest取得响应

* responseText:获得字符串形式的响应数据
* responseXML：获得XML形式的响应数据（比较少）
* status和statusText:以数字和文本形式返回HTTP状态码 
* getAllResponseHeader()：获取所有的响应报头
* getResponseHeader()：查询响应中的某个字段的值

readyState属性的变化代表服务器响应的变化
0：请求未初始化，open还没有调用
1：服务器连接已建立，open已经调用了
2：请求已接收，也就是接收到头信息了
3：请求处理中，也就是接收到了响应主体
4：请求已完成，且响应已就绪，也就是响应完成了

var request = new XMLHttpRequest() //建立XHR对象
request.open("GET","get.php",true); //用get方法异步打开get.php
request.send(); //发送请求头信息
request.onreadystatechange=function(){
if(request.readState===4&&request.status===200){
//做一些事情 request.responseText;
}
}

通过onreadystatechange事件 ，对readyState属性进行监听即对服务器的响应进行监听，
readyState===4响应完成；
status===200，请求成功

建立异步请求的过程4个步骤：
a:new一个XHR对象
b:调用open方法
c:send一些数据
d:对过程进行监听，来知道服务器是不是正确地做出了响应，接着可以做一些事情
（监听readyState,响应成功可以做一些事情，比如获取服务器响应的内容在页面上做一些呈现）