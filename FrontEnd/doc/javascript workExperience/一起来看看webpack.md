一起来看看webpack吧！！！ 学习笔记
--
> 引用自 http://www.jianshu.com/p/b95bbcfc590d

**1.WebPack是什么？**

　　1.一个打包工具

　　2.一个模块加载工具

　　3.各种资源都可以当成模块来处理

**2.WebPack主要特点是什么**
	
1.丰富的插件，方便进行开发工作  
2.大量的加载器，包括加载各种静态资源  
3.代码分割，提供按需加载的能力  
4.发布工具  

**3.WebPack的优势**  
1.webpack 是以 commonJS 的形式来书写脚本滴，但对 AMD/CMD 的支持也很全面，方便旧项目进行代码迁移。	  

2.开发便捷，能替代部分 grunt/gulp 的工作，比如打包、压缩混淆、图片转base64等。  

3.扩展性强，插件机制完善，特别是支持 React 热插拔（见 react-hot-loader ）的功能让人眼前一亮。

**4.WebPack的安装**

1.安装命令

	 $ npm install webpack -g

2.使用webpack

	 $ npm init  # 会自动生成一个package.json文件
	 $ npm install webpack --save-dev
	// 将webpack增加到package.json文件中`


**5.WebPack的配置**


每个项目下都必须配置有一个 webpack.config.js ，它的作用如同常规的 gulpfile.js/Gruntfile.js ，就是一个配置项，告诉 webpack 它需要做什么。


下面是一个例子:

		var webpack = require('webpack');
		var commonsPlugin = new webpack.optimize.CommonsChunkPlugin('common.js');
		module.exports = {
    	//插件项
	    plugins: [commonsPlugin],
	    //页面入口文件配置
	    entry: {
	        index : './src/js/page/index.js'
	    },
	    //入口文件输出配置
	    output: {
	        path: 'dist/js/page',
	        filename: '[name].js'
	    },
	    module: {
	        //加载器配置
	        loaders: [
	            { test: /\.css$/, loader: 'style-loader!css-loader' },
	            { test: /\.js$/, loader: 'jsx-loader?harmony' },
	            { test: /\.scss$/, loader: 'style!css!sass?sourceMap'},
	            { test: /\.(png|jpg)$/, loader: 'url-loader?limit=8192'}
	        ]
	    },
	    //其它解决方案配置
	    resolve: {
	        root: 'E:/github/flux-example/src', //绝对路径
	        extensions: ['', '.js', '.json', '.scss'],
	        alias: {
	            AppStore : 'js/stores/AppStores.js',
	            ActionType : 'js/actions/ActionType.js',
	            AppAction : 'js/actions/AppAction.js'
	        }
	    }
	};


1.plugins 是插件项，这里我们使用了一个 CommonsChunkPlugin的插件，它用于提取多个入口文件的公共脚本部分，然后生成一个 common.js 来方便多页面之间进行复用。


2.entry 是页面入口文件配置，output 是对应输出项配置 （即入口文件最终要生成什么名字的文件、存放到哪里）

3.module.loaders 是最关键的一块配置。它告知 webpack 每一种文件都需要使用什么加载器来处理。 所有加载器需要使用npm来加载


4.最后是 resolve 配置，配置查找模块的路径和扩展名和别名（方便书写）



简单的一次配置实验：


1.正确安装了WebPack，方法可以参考上面

2.书写entry.js文件

	 document.write(require("./content.js"));

3.书写index.html文件

	<html>
	<head>
	<meta charset="utf-8">
	</head>
	<body>
	<script type="text/javascript" src="bundle.js" charset="utf-8"></script>
	</body>
	</html>


4.增加一个content.js文件

	module.exports = "现在的内容是来自于content.js文件！";


5.增加style.css文件
	
	body {
	background: yellow;
	}

6.修改entry.js文件
	require("!style!css!./style.css");
	document.write(require("./content.js"));

7.执行命令，安装加载器
	
	$ npm install css-loader style-loader   # 安装的时候不使用 -g

8.增加webpack.config.js文件

	module.exports = {
	 entry: "./entry.js",
	 output: {
	     path: __dirname,
	     filename: "bundle.js"
	 },
	 module: {
	     loaders: [
	         { test: /\.css$/, loader: "style!css" }
	     ]
	 }
	};


9.执行程序
	
	$ webpack