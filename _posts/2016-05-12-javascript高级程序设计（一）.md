---
layout: default
title: javascript高级程序设计（一）
category: javascript
---
<h2>javaScript高级程序设计（一）</h2>
<h3>1、script标签属性：defer vs async</h3>
先放一篇简单易懂的博文[defer vs async](http://www.growingwiththeweb.com/2014/02/async-vs-defer-attributes.html)

* 当没有defer和async属性时，每遇到script标签则阻塞html的解析，下载并执行js，之后再解析html
* 当有async时，异步加载js，加载的同时解析html，但是当js加载完毕的时候会阻塞html的解析转而执行js，js执行完毕再继续解析html，不保证js文件会按顺序执行。
* 当有defer时，异步加载js文件，下载完的js文件并不会立即执行，而是被挂起，等浏览器解析完html之后再执行，而且defer保证js文件按顺序执行（但现实中好像并不是这样）。

<h3>2、boolean值的自动转换</h3>
```javascript
var message = "hello world";
if(message){
	alert("Value is true");
}
```
如上：在控制流语句中，在判断条件中会自动进行boolean值的转换，引擎会自动调用boolean(message)方法对条件进行boolean值转换。

<h3>3、isFinite()</h3>
该方法可以用来检测一个数值是否在浏览器允许的最大整数和最小整数之间。

<h3>4、toString()方法</h3>
该方法的作用是将任意的数值或者boolean等转换为字符串，而toString方法允许传递一个参数：输出数值等基数；即可以通过传递这个参数将十进制数值转换为任意进制的数。

```javascript
10.toString(8);	// 12(八进制)
```

**注：null和undefined没有toString方法。**

<h3>5、逻辑与、逻辑或</h3>
逻辑与和逻辑或这两个操作符都是短路运算符，逻辑与是当第一个运算为false的时候短路，逻辑或是当第一个运算为true的时候发生短路。
