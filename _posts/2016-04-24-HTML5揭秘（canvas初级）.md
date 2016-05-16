---
layout: default
title: HTML5揭秘（初级canvas）
category: HTML
excerpt: 本文主要介绍初级的canvas（以前没有使用过canvas，捂脸.png）
---

<h2>HTML5揭秘(初级Canvas)</h2>
<h3>1、简单图形</h3>

```html
<canvas id="ca" width="200" height="200"></canvas>
```
```javascript
var canvas = document.getElementById("ca");
var c_context = canvas.getContext("2d");
c_context.fillRect(x,y,width,height);
```

**下面的都是context的方法**

* fillStyle:可以设置为css颜色，图案或者渐变色，默认为黑色
* fillRect(x,y,width,height): 绘制一个矩形，并以当前的fillStyle来填充
* strokeStyle，同fillStyle
* strokeRect(x,y,width,height): 同fillRect，只不过不会填充中间内容区域，只绘制矩形的边缘
* clearRect(x,y,width,height): 清除指定区域的矩形
* moveTo(x,y): 将绘制点移到x，y处
* lineTo(x,y): 从绘制起始点绘制一条到x,y处的不可见的线，这里说不可见是因为需要下面的stroke方式绘制到画布上。
* stroke(): 将moveTo和lineTo绘制的不可见的线在canvas上呈现出来，在调用此方法前可以调用context.strokeStyle设置填充色

<h3>2、字体相关</h3>

* font: 用来设置字体size，style，weight，line-height,font-family
* textAlign: start,end,left,right,center
* fillText("font",x,y): fillText方法用来绘制实际点文本，font为要绘制点文本，xy为要绘制文本的起始位置

<h3>3、渐变</h3>

```javascript
var context = document.getElementById("canvas").getContext("2d");
// 创建渐变对象
var myGradient = context.createLinearGradient(x1,y1,x2,y2);
// 添加渐变的颜色,0为起始色值，1为终止色值，可以增加任意数量的色值，取值0-1之间
myGradient.addColorStop(0, "black");
myGradient.addColorStop(1, "white");
// 此时的渐变只是存在于内存中，可以作为fillStyle或者strokeStyle的值，只有调用context的绘制方法才能绘制到canvas上
context.fillStyle = myGradient;
context.fillRect(0,0,100,100);
```

<h3>4、图片</h3>
调用context的drawImage()方法可以在canvas中绘制一张图片并且可以对图片进行裁剪。图片在canvas中放置的坐标点为图片左上角的位置。

* drawImage(img,x,y): 将img放置到xy位置
* drawImage(img,x,y,w,h): 同上，wh表示缩放到宽高为w，h
* drawImage(img,sx,sy,sw,sh,dx,dy,dw,dh): (sx,sy,sw,sh)为在sx，sy位置裁剪宽度为sw，高度为sh的区域，（dw，dh）为缩放后的大小，（dx，dy）为在canvas中放置的坐标

如果是通过javascript创建图片，则可以通过image.onload方法将图片安全地放到canvas中

```javascript
var image = new Image();
image.src = 'url*.png';
image.onload = function() {
 	context.drawImage(image,x,y);
}
```