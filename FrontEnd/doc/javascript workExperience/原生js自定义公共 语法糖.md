原生js自定义公共 语法糖
--

	//实例
		(function(){
		    var common = function(){};
		    common.prototype.helloName =  function(){
		        console.log(123);
		    }
		    window.$$ = new common();
		})()
		
		$(function(){
		    $$.helloName();
		})		