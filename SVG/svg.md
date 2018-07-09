# 概述
- svg：可缩放矢量图形
- svg：用来定义网络的基于矢量的图形
- svg：使用XML格式定义图像
- svg：图像在放大或改变尺寸的情况下不会有所损失

# 实例
```xml
<?xml version="1.0" standalone="no"?>

<!DOCTYPE svg PUBLIC "-//W3C//DTD SVG 1.1//EN"
"http://www.w3.org/Graphics/SVG/1.1/DTD/svg11.dtd">

  <svg width="100%" height="100%" version="1.1"
  xmlns="http://www.w3.org/2000/svg">

  <circle cx="100" cy="50" r="40" stroke="black"
  stroke-width="2" fill="red"/>

</svg>
```

# SVG嵌入到HTML
- embed标签
```xml
<embed src="rect.svg" width="300" height="100"
type="image/svg+xml"
pluginspage="http://www.adobe.com/svg/viewer/install/" />
```
- object标签(不允许使用脚本)
```xml
<object data="rect.svg" width="300" height="100"
type="image/svg+xml"
codebase="http://www.adobe.com/svg/viewer/install/" />
```
- iframe标签
```xml
<iframe src="rect.svg" width="300" height="100"></iframe>
```

# SVG形状
- 矩形 rect
- 圆形 circle
- 椭圆 ellipse
- 线 line
- 折线 polyline
- 多边形 polygon
- 路径 path
