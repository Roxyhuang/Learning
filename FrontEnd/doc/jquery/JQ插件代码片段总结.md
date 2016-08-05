JQ插件代码片段总结
--

jQuery为开发插件提拱了两个方法，分别是： 

jQuery.extend(object);为扩展jQuery类本身.为类添加新的方法。 
jQuery.fn.extend(object);给jQuery对象添加方法。 


	(function($){
	    //少量参数
	    $.fn.helloName = function(name,age){
	        this.text("名字:"+name+"年龄:"+age);
	        return this;
	    };
	    //对象参数
	    $.fn.helloPerson = function (option){
	        this.text("名字:"+option.name+"年龄:"+option.age);
	        return this;
	    };
	    //默认参数并且合并
	    $.fn.helloFriend = function(option){
	        var defaultOption =  {name:"张三",age:22};
	        $.extend(defaultOption,option);
	        this.text("名字："+defaultOption.name+"年龄："+defaultOption.age);
	        return this;
	    }
	
	})(jQuery);
	
	
	//extend 扩展
	(function($){

    $.fn.extend({
        name:"张三",
        age:13,
        clickAlert :function(){
            alert(this.name+this.age);
        }
    });
	})(jQuery);



	(function(){
	    $("body").helloName("张三",22);
	    $("body").helloPerson({name:"王二麻",age:16});
	    $("body").helloFriend({age:16});
    $("#button1").on("click",function(){
        $("#button1").clickAlert();
    })
	})();