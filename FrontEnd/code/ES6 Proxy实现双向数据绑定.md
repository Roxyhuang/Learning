ES6 Proxy实现双向数据绑定
--


	 var engineer = { name: 'Joe Sixpack', salary: 50 };
	    //定义处理程序
	    var interceptor = {
	        set: function (receiver, property, value) {
	            console.log(property, 'is changed to', value);
	            receiver[property] = value;
	        }
	    };
	    //创建代理以进行侦听
	    engineer = new Proxy(engineer, interceptor);
	    //做一些改动来触发代理
	    engineer.salary = 60;