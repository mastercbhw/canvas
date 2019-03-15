# canvas相关API

``` javascript
const canvas = document.getELementById('canvas') // 获取canvas dom
const context = canvas.getContext('2d') // 获取到这个 Canvas 的上下文对象：
```


### arc() 方法创建弧/曲线（用于创建圆或部分圆）

``` javascript
context.arc(x,y,r,sAngle,eAngle,counterclockwise);
```
- x：圆心的 x 坐标
- y：圆心的 y 坐标
- r：圆的半径
- sAngle：起始角，以弧度计（弧的圆形的三点钟位置是 0 度）
- eAngle：结束角，以弧度计
- counterclockwise：可选。规定应该逆时针还是顺时针绘图。false 为顺时针，true 为逆时针


### fill()和stroke()

fill()是填充,stroke()是描边

相应的对应 fillStyle和strokeStyle

![Image text](./image/fill-stroke.png)


### moveTo(x,y)

把路径移动到画布中的指定点，不创建线条


### lineTo(x,y)

添加一个新点，然后在画布中创建从该点到最后指定点的线条

> 如果没有 moveTo，那么第一次 lineTo 的就视为 moveTo
> 每次 lineTo 后如果没有 moveTo，那么下次 lineTo 的开始点为前一次 lineTo 的结束点。

## 在绘制了直线之后，我们来看一下怎么给绘制的直线添加样式

|样式|	描述|
|:---|:---|
|lineCap|	设置或返回线条的结束端点样式
|lineJoin|	设置或返回两条线相交时，所创建的拐角类型
|lineWidth|	设置或返回当前的线条宽度
|miterLimit|	设置或返回最大斜接长度

- **lineCap**

|值 | 描述|
|:--|:--|
|butt	|默认。向线条的每个末端添加平直的边缘。
|round	|向线条的每个末端添加圆形线帽。
|square|	向线条的每个末端添加正方形线帽。

- **lineJoin**

lineJoin 属性设置或返回所创建边角的类型，当两条线交汇时。

|值|	描述|
|:--|:--|
|bevel|	创建斜角。|
|round|	创建圆角。|
|miter|	默认。创建尖角。|


### fillRect(x, y, width, height) 和strokeRect(x, y, width, height)

> 通过 fillStyle() 和 strokeStyle() 来设置填充的颜色和描边的颜色。


## 颜色、样式和阴影

|属性|	描述|
|:--|:--|
|fillStyle|	设置或返回用于填充绘画的颜色、渐变或模式|
|strokeStyle|	设置或返回用于笔触的颜色、渐变或模式|
|shadowColor|	设置或返回用于阴影的颜色|
|shadowBlur|	设置或返回用于阴影的模糊级别|
|shadowOffsetX|	设置或返回阴影距形状的水平距离|
|shadowOffsetY|	设置或返回阴影距形状的垂直距离|

## 设置渐变

|方法	|描述|
|:-|:-|
|createLinearGradient()|	创建线性渐变（用在画布内容上）|
|createPattern()|	在指定的方向上重复指定的元素|
|createRadialGradient()|	创建放射状/环形的渐变（用在画布内容上）|
|addColorStop()|	规定渐变对象中的颜色和停止位置|

demo
``` javascript
var canvas = document.getElementById("canvas");
var context = canvas.getContext("2d");
var cx = canvas.width = 400;
var cy = canvas.height = 400;

var grd = context.createLinearGradient(0,0,0,400);
grd.addColorStop(0,'rgb(255, 0, 0)');
grd.addColorStop(0.2,'rgb(255, 165, 0)');
grd.addColorStop(0.3,'rgb(255, 255, 0)');
grd.addColorStop(0.5,'rgb(0, 255, 0)');
grd.addColorStop(0.7,'rgb(0, 127, 255)');
grd.addColorStop(0.9,'rgb(0, 0, 255)');
grd.addColorStop(1,'rgb(139, 0, 255)');

context.fillStyle = grd;
context.fillRect(0,0,400,400);
```


## 图形转换

|方法  |	描述|
|:--|:--|
|scale()|	缩放当前绘图至更大或更小|
|rotate()|	旋转当前绘图|
|translate()|	重新映射画布上的 (0,0) 位置|
|transform()|	替换绘图的当前转换矩阵|
|setTransform()|	将当前转换重置为单位矩阵，然后运行 transform()|


## 图形绘制

图像绘制
Canvas 还有一个经常用的方法是drawImage()。

|方法	|描述|
|:--|:--|
|drawImage()|向画布上绘制图像、画布或视频|

> context.drawImage(img,sx,sy,swidth,sheight,x,y,width,height);

- img：规定要使用的图像、画布或视频
- sx：可选。开始剪切的 x 坐标位置
- sy：可选。开始剪切的 y 坐标位置
- swidth：可选。被剪切图像的宽度
- sheight：可选。被剪切图像的高度
- x：在画布上放置图像的 x 坐标位置
- y：在画布上放置图像的 y 坐标位置
- width：可选。要使用的图像的宽度（伸展或缩小图像）
- height：可选。要使用的图像的高度（伸展或缩小图像）

**注意点**
 /**等图片资源加载完成后，才在 Canvas 上进行绘制渲染*/
``` javascript
img.onload = function () {
  context.drawImage(img, 0, 0);
}
```