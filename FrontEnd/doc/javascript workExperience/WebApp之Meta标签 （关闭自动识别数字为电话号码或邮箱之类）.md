iPhone上的Safari(还有些webkit android手机浏览器)会自动对看起来像是电话号码的数字串（包括已经加入连字符或括号格式化过的）添加电话链接，点击之后会询问用户是否想要拨打该号码。如果你不希望开启这个自动识别，可以将它关闭：

<meta name="format-detection" content="telephone=no" />

如果你关闭自动识别后，又希望某些电话号码能够链接到iPhone的拨号功能，那么可以通过这样来声明电话链接：
<a href="tel:13800138000">13800138000</a>
 
<meta content="email=no" name="format-detection" />//将不识别邮箱
 
<meta name="apple-mobile-web-app-capable" content="yes" />
这meta的作用就是删除默认的苹果工具栏和菜单栏。content有两个值”yes”和”no”,当我们需要显示工具栏和菜单栏时，这个行meta就不用加了，默认就是显示。

<meta name=”apple-mobile-web-app-status-bar-style” content=black” /> 
默认值为default（白色），可以定为black（黑色）和black-translucent（灰色半透明）。
注意： 若值为“black-translucent”将会占据页面px位置，浮在页面上方（会覆盖页面20px高度–iphone4和itouch4的Retina屏幕为40px）。
 
iOS用rel="apple-touch-icon",android 用rel="apple-touch-icon-precomposed"。这样就能在用户把网页存为书签时，在手机HOME界面创建应用程序样式的图标。
<link rel="apple-touch-icon" href="/static/images/identity/HTML5_Badge_64.png" />
<link rel="apple-touch-icon-precomposed" href="/static/images/identity/HTML5_Badge_64.png" />
