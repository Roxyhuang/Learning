web离线存储
--
>引用自：
> https://segmentfault.com/a/1190000000732617
> http://mp.weixin.qq.com/s?__biz=MzA4ODIxMzg5MQ==&mid=2653995942&idx=1&sn=87f21b6412eeede0d5ee7dc2f6e153d2&scene=23&srcid=0716KPoErhXR84AvSpKqiHD8#rd
> http://mp.weixin.qq.com/s?__biz=MzAwNjI5MTYyMw==&mid=2651493111&idx=1&sn=7092d3a0527a726488c5a1c02bc0c808&scene=23&srcid=07188rpV7ZCnjQNzgJKmkJSM#rd
> http://www.codeceo.com/article/html5-cache.html

在用户没有与因特网连接时，可以正常访问站点或应用，在用户与因特网连接时，更新用户机器上的缓存文件。
原理：HTML5的离线存储是基于一个新建的.appcache文件的缓存机制(不是存储技术)，通过这个文件上的解析清单离线存储资源，这些资源就会像cookie一样被存储了下来。之后当网络在处于离线状态下时，浏览器会通过被离线存储的数据进行页面展示。

如何使用:

1、页面头部像下面一样加入一个manifest的属性；

2、在cache.manifest文件的编写离线存储的资源；

	    CACHE MANIFEST
	    #v0.11
	    CACHE:
	    js/app.js
	    css/style.css
	    NETWORK:
	    resourse/logo.png
	    FALLBACK:
	    / /offline.html

3、在离线状态时，操作window.applicationCache进行需求实现。

