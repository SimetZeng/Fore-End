# 概述
Qunee for HTML5是一种一种**Web图形解决方案**
Qunee可用于拓扑图，流程图，组织图，机房平面图，组态软件的开发，具有轻量、高效、灵活扩展的特点，支持目前主流浏览器（Safari, Firefox, Chrome, IE9+），可运行在不同操作系统（Windows, Mac, Linux......）和移动终端（iOS，Android，Windows Phone......），借助PhoneGap之类的移动开发框架，可以开发移动应用程序

**Qunee提供Web图形解决方案**
- 地图 - 地铁图、统计地图
- 拓扑图 - 社交网络图、网络管理图
- 其他 - 组织图、思维导图、流程图


**Qunee组件的特点**
- 轻巧、高性能 - 支持上万图元，流畅操作
- 矢量图形 - 支持矢量图形，无极缩放
- 交互体验 - 漫游交互，改进交互事件、支持手持设备
- 注重细节 - GIF动画，丰富渐变，层次控制等

**浏览器支持**
Google Chrome（推荐）, Firefox, Safari, IE9+

**使用Qunee开发应用通常按下面的流程**
数据采集 --> 数据转换 --> 数据呈现 --> 交互监听 --> 数据操作 --> 数据提交（其中与Qunee直接相关的是中间的四部分）

数据转换：
1. 转换成JS对象
```javascript
function onDataCollected(txt){
  var json = JSON.parse(txt);
  translateToQuneeElements(json);
}
```

2. 转换成Qunee图元
Qunee图形组件中的**图形都有对应的模型对象**，称为Qunee图元，用户数据需要先转换成这种元素，才能在Qunee图形组件中展示，Qunee元素有多种类型，支持丰富的呈现样式和扩展方式，不同的数据根据其显示意图转换成不同类型的Qunee图元，并设置相应的图形样式，特殊展示效果的可以通过UI扩展来实现

将JSON对象转换成Qunee元素，并添加到图形容器
```javascript
function translateToQuneeElements(json, graph){
  var map = {};
  if(json.nodes){
      Q.forEach(json.nodes, function(data){
          var node = graph.createNode(data.name, data.x || 0, data.y || 0);
          node.set("data", data);
          map[data.id] = node;
      });
  }
  if(json.edges){
      Q.forEach(json.edges, function(data){
          var from = map[data.from];
          var to = map[data.to];
          if(!from || !to){
              return;
          }
          var edge = graph.createEdge(data.name, from, to);
          edge.set("data", data);
      }, graph);
  }
}
```

3. 数据呈现
数据转换成Qunee元素对象，添加到图形组件后，便可以查看呈现效果了
```javascript
var graph = new Q.Graph("canvas");
function onDataCollected(txt){
    var json = JSON.parse(txt);
    translateToQuneeElements(json);
    graph.moveToCenter();
}
function translateToQuneeElements(json){
    if(json.nodes){
        Q.forEach(json.nodes, toQuneeNode);
    }
    if(json.edges){
        Q.forEach(json.edges, toQuneeEdge);
    }
}
//... ajax请求接口数据
```
# 图形元素
## 图元基类
图形元素基类为：Q.Element，简称图元，提供了基本的图元支持，提供了事件监听、属性支持、父子关系等基本功能，在此之上提供了两种基本图元：Q.Node，Q.Edge，分别用于描述节点和连线，在图论中Node代表点，Edge代表边，节点通过连线相连，两个节点之间可以存在多条连线， 此外还有些扩展类型：Q.Group, Q.Text, Q.ShapeNode等
