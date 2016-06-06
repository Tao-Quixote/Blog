---
layout: default
title: javaScript高级程序设计（二）
category: JavaScript
excerpt: javaScript高级程序设计系列第二发，主要是一些关于数组操作的方法。
---

<h2>javaScript高级程序设计（二）</h2>

<h3>1、对象属性访问</h3>
两种方法，第一种方法是通过“.”来访问对象的属性，第二种方法是通过“［］”来访问对象的属性，从功能上来说两种方法都试一样的，但是“［］”允许开发者使用变量或者带有非字母和数字的属性名。

```javascript
var attr = 'attr name';
obj[attr]  |  obj['attr name'];
```

当然，并不推荐使用带有非字母或者数字的属性名。除非使用变量来访问属性，推荐使用点来访问属性。

<h3>2、数组相关方法</h3>

* push：对数组执行压栈操作
* pop：对数组执行弹栈操作
* shift：弹出数组第一个值
* unshift：在数组的头部加入任意的值
* reverse：翻转数组
* sort：对数组排序，默认为将数组所有值调用toString方法后再比较排序(所以会产生15排在2前面的情况)，可传入一个比较方法，如果val1 > val2则返回负数，如果相等则返回0，如果val2 < val1则返回正数，例：

```javascript
function compare(val1, val2) {
	if(val1 < val2) {
		return -1;
	} else if(val1 == val2) {
		return 0;
	} else {
		return 1;
	}
}
```

<h3>3、数组插入和替换方法splice</h3>
最强大的数组方法

* 删除: arr.splice(start, num),start为要删除的起始项的index，num为删除项的个数
* 替换: arr.splice(start,1,replacement),其实并不是操作，而是在指定位置删除了一项，然后在指定位置又插入了一项，伪替换
* 插入: arr.splice(start,0, [...]),在指定位置插入任意项

<h3>4、数组迭代方法</h3>

```javascript
function iterate(item, index, arr) { 
	...
}
```

* every(iterate): 如果每次运行回调的返回值都是true，则every运行结果返回true
* some(iterate): 如果有任意一次运行回调的返回值是true，则some的运行结果返回true
* filter(iterate): 对每一项运行回调，该方法返回回调结果为true的项组成的数组
* forEach(iterate): 没有返回值，与for一样，只是遍历数组
* map(iterate): 返回每次运行回调返回的值组成的数组

<h3>5、reduce vs reduceRight</h3>
这两个方法都会迭代数组的所有项，然后构建一个最终返回的值。reduce方法从数组的第一项开始，reduceRight从数组的最后一项开始，接收一个回调，回调如下：

```javascript
function re(prev, cur, index, array) {
	...
}
```
主要用于将数组中的值遍历后做相加或者类似的操作，感觉跟forEach方法差不多。