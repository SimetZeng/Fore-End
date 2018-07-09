# openlayer - Web Gis 引擎

# 概述
OpenLayers 3简称ol3，是一个开源的Web GIS引擎，使用了JavaScript、HTML5及CSS3技术。在地图数据源方面，支持各种类型的瓦片地图，既支持在线的，也支持离线的。


# 支持浏览器

由于OpenLayers 3使用了HTML5技术，所以对各种浏览器的版本有所要求。IE浏览器最低需要IE9，IE9以下的浏览器可以考虑使用OpenLayers 2。其他浏览器的最低版本要求：Firefox 3.5，Chrome 3.0，Safari 3.0，Opera 10.5。

# 'Hello World'

```
//想要使用OpenLayers 3，首先你需要引入了ol3的js库文件ol.js及样式文件ol.css。
<link ref="stylesheet" href="./ol.ol.css" type="text/css"></link>
<script src="./ol/ol.js"></script>

//指定容器
<div id="map" style="width: 100%"></div>

<script>
   // 创建地图
   let mapObj = new ol.Map({
      // 设置地图图层
      layers: [
          // 创建地图源为Open Street Map瓦片图层
          new ol.layer.Tile({source: new ol.source.OSM()})
        ],
        // 设置地图的视图
        view: new ol.View({
           center: [0, 0],    // 定义地图显示中心于经度0度，纬度0度处
           zoom: 2            // 并且定义地图显示层级为2
        }),
        // 指定地图在页面具体的位置进行显示，所以要记住
        // 地图显示还是离不开使用dom来实现。虽然和地图业务没关系，但也必不可少，
        // 因为它是Web GIS，最基本的还是依赖于HTML。
        target: 'map'
    });
 </script>
