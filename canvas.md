# Canvas
```<canvas width height></canvas>```
* 绘画上下文 drawing.getContext(“2d”)
* 导出图像img.src=drawing.toDataURL(“image/png”)
* 原点坐标左上角
  * fillStyle 
  * strokeStyle 
  * fillRect 
  * clearRect
  * beginPath()
  * arc(x,y,半径，起始角度，结束角度，逆时针)
  * arcTo(x1,y1,x2,y2,半径):至(x2,y2)，以半径穿过(x1,y1)
  * bezierCurveTo(c1x,c1y,c2x,c2y,x,y)至(x,y)过c1 c2
  * lineTo(x,y) 
  * moveTo(x,y)
  * quadraticCurveTo(cx,cy,x,y):二次曲线到(x,y)，过(cx,cy)
  * rect(x,y,width,height):矩形路径
  * closePath():连接到路径起点
  * fill() 
  * stroke() 
  * clip()
  * isPointInPath(100,100) 路径被关闭之前 某一点是否位于路径上
  * fillText 
  * strokeText(内容，x,y,最大像素)
  * font 
  * textAlign(start end) 
  * textBaseline
  * measureText(内容).width
  * rotate(弧度) 
  * scale(缩放比例x y) 
  * translate(x,y)将坐标原点移动到x,y 
  * save() 保存设置 
  * restore() 
  * drawImage(img,x,y)
  * drawImage(img,x,y,宽,高) 改变绘制后图像大小
  * drawImage(canvas,源x,源y,源宽,源高,x,y,宽,高)
  * shadowColor 
  * shadowOffsetX 
  * shadowOffsetY 阴影偏移量  
  * shadowBlur 模糊像素数
  * createLinearGradient(30,30,70,70)
  * createRadialGradient(x1,y1,半径1，x2,y2,半径2)
  * addColorStop(0/1,”white”)
  * context.fillStyle/strokeStyle=gradient;
  * createPattern(img/canvas/video,repeat/repeat-x/repeat-y/no-repeat);
  * context.fillStyle=pattern
  * getImageData(x,y,宽度,高度) 三个属性 width height data
    * data 数组，每一像素的数据
  * 灰阶过滤 i+=4  data[i] data[i+1] data[i+2] data[i+3]
    * data[i]/data[i+1]/data[i+2]=average;
    * 去掉颜色，保留亮度
    * putImageData(imageData,x,y);
* canvas优化
  * 离屏 Canvas:createElement('canvas')
    * 不需要反复图片渲染
    * 只要一个图，然后自适应 drawImage(canvas, 0, 0);
  * 集中绘制 绘制操作 消耗资源
    * beginPath() 一堆操作 stroke()
  * 不变的场景分离变化的物体
    * 背景图置于canvas后
  * 坐标点浮点数 浏览器额外的运算
