Page Visibility 的学习笔记
--
> 引用 http://www.tuicool.com/articles/BfIjYf

不知道用户是不是在与页面交互，这是困扰广大 Web 开发人员的一个主要问题。如果 页面最小化了 或者 隐藏在了其他标签页后面 ，那么有些功能是可以停下来的，比如轮询服务器或者某些动画效果。那么如何判断呢？


H5 之前，我们可以监听 onfocus() 事件。如果当前窗口得到焦点，那么我们可以简单认为用户在与该页面交互，如果失去焦点（ onblur() ），那么可以认为用户停止与该页面交互。

	// 当前窗口得到焦点
	window.onfocus = function() {
	  // 动画
	  // ajax 轮询等等
	};
	
	// 当前窗口失去焦点
	window.onblur = function() {
	  // 停止动画
	  // 停止 ajax 轮询等等
	};


但是这样的方法显然是很 "粗糙" 的。思考这样一个场景，一边打开浏览器看视频，一边撸代码，很显然，焦点集中在编辑器中，那么浏览器失去焦点，就意味着用户没在与页面交互了吗？



H5 引入的 Page Visibility API，能很有效地帮助我们完成这样的判断。

这个 API 本身非常简单，由以下三部分组成。

document.hidden：表示页面是否隐藏的布尔值。页面隐藏包括 页面在后台标签页中 或者 浏览器最小化 （注意，页面被其他软件遮盖并不算隐藏，比如打开的 sublime 遮住了浏览器）

document.visibilityState：表示下面 4 个可能状态的值
hidden：页面在后台标签页中或者浏览器最小化
visible：页面在前台标签页中
prerender：页面在屏幕外执行预渲染处理 document.hidden 的值为 true
unloaded：页面正在从内存中卸载
Visibilitychange 事件：当文档从可见变为不可见或者从不可见变为可见时，会触发该事件。

这样，我们可以监听 Visibilitychange 事件，当该事件触发时，获取 document.hidden 的值，根据该值进行页面一些事件的处理。

    document.addEventListener("visibilitychange",function(){
        var isHidden = document.hidden,
             isVisible = document.visible,
             isPrerender = document.prerender;
             isUnloaded  = document.unloaded;
        if (isHidden) {
            console.log("隐藏");
        }
        if(isVisible){
            console.log("显示")

        }
        if(isPrerender){
            console.log("预渲染");
        }
    })




	提供一个兼容各高级浏览器以及低版本 IE 写法（低版本 IE 用 onfocus/onblur 兼容）：
	
	(function() {
	  var hidden = "hidden";
	
	  // Standards:
	  if (hidden in document)
	    document.addEventListener("visibilitychange", onchange);
	  else if ((hidden = "mozHidden") in document)
	    document.addEventListener("mozvisibilitychange", onchange);
	  else if ((hidden = "webkitHidden") in document)
	    document.addEventListener("webkitvisibilitychange", onchange);
	  else if ((hidden = "msHidden") in document)
	    document.addEventListener("msvisibilitychange", onchange);
	  // IE 9 and lower:
	  else if ("onfocusin" in document)
	    document.onfocusin = document.onfocusout = onchange;
	  // All others:
	  else
	    window.onpageshow = window.onpagehide
	    = window.onfocus = window.onblur = onchange;
	
	  function onchange (evt) {
	    var v = "visible", h = "hidden",
	        evtMap = {
	          focus:v, focusin:v, pageshow:v, blur:h, focusout:h, pagehide:h
	        };
	
	    evt = evt || window.event;
	    if (evt.type in evtMap)
	      document.body.className = evtMap[evt.type];
	    else
	      document.body.className = this[hidden] ? "hidden" : "visible";
	  }
	
	  // set the initial state (but only if browser supports the Page Visibility API)
	  if( document[hidden] !== undefined )
	    onchange({type: document[hidden] ? "blur" : "focus"});
	})();



http://www.jb51.net/article/40857.htm


js中onload与onunload的使用示例


	<script> 
	window.onunload = function(){if(self.screenTop>9000)alert('该窗口已经被关闭！')} 
	</script> 
	或 
	<script> 
	window.onunload = function(){if(self.screenLeft>9000)alert(该窗口已经被关闭！.')} 
	</script> 


	<body 
	onunload="javascript:if(self.screenTop>9000) window.location.href='${pageContext.request.contextPath }/cart/closeWindow.action';"> 