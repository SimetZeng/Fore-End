# 地图打点

<!-- TOC depthFrom:1 depthTo:6 withLinks:1 updateOnSave:1 orderedList:0 -->

- [地图打点](#地图打点)
- [概述](#概述)
	- [Vector Labels](#vector-labels)
	- [Overlay Labels](#overlay-labels)

<!-- /TOC -->
# 概述
地图打点分2种标注类型
* Vector Labels
* Overlay Labels

## Vector Labels
```javascript
let vectorSource = new ol.source.Vector();

let iconFeature = new ol.Feature({
    geometry: new ol.geom.Point([113.1231, 22.23422]),
    id: 1
});

let mark = new ol.style.Style({
    image: new ol.style.Icon({
        anchor: [0.5, 0.5],
        anchorOrigin: 'top-right',
        anchorXUnits: 'fraction',
        anchorYUnits: 'pixels',
        offsetOrigin: 'top-right',
        src: 'mark.png'
    })
});

iconFeature.setStyle(mark);
vectorSource.addFeature(iconFeature);

//添加以下这段可实现聚合功能
//聚合标记数据源
let clusterSource = new ol.source.cluster({
    distance: 40,//聚合的距离，当大于等于这个值时图标聚合
    source: vectorSource
});

let styleCache = {};
//创建矢量标注图层
let clusters = new ol.layer.Vector({
    source: clusterSource,
    style: funtion (feature, resolution) {
        let size = feature.get('features').length;//当前聚合的点个数
        let style = styleCache[size];
        let imgSrc = 'singleMark.png';
        let fill = new ol.style.Fill({color: '#d81e06'});//文本填充样式
        let offsetY = -18;
        if (size > 1) {
            imgSrc = 'cluster.png';
            fill = new ol.style.Fill({color: 'black'});
            offsetY = -15;
        }
        if (!style) {
            style = [new ol.style.Style({
                image: new ol.style.Icon(({
                    anchor: [0.5, 0.5],
                    anchorOrigin: 'bottom-left',
                    anchorXUnits: 'fraction',
                    anchorYUnits: 'pixels',
                    offsetOrigin: 'bottom-left',
                    src: imgSrc
                })),
                text: new ol.style.Text({
                    offsetY: offsetY,
                    textAlign: 'center',
                    textBaseline: 'bottom',
                    font: 'bold 14px 微软雅黑',
                    text: size.toString(),
                    fill: fill
                })
            })];
        }
    }
});
//聚合代码到此结束


let vectorLayer = new ol.layer.Vector({
    source: vectorSource
});

map.addLayer(vectorLayer);
```


## Overlay Labels

```javascript
<div id="marker"><img src="../img/marker.png"/></div>

<script type="text/javascript">
  var mapObj = new ol.Map({
    layers: [
      new ol.layer.Tile({
        source: new ol.source.OSM()
      })
    ],
    target: 'map',
    view: new ol.View({
      projection: 'EPSG:4326',
      center: [0, 0],
      zoom: 10
  });

  // 下面把上面的图标附加到地图上，需要一个ol.Overlay
  let marker = new ol.Overlay({
    position: [0, 0],
    element: document.getElementById('marker')
  });
  // 然后添加到map上
  mapObj.addOverlay(marker);
</script>
```

## 说明
Overlay Labels适合点较少的情况，因为毕竟是操作了dom，点一多界面就会卡顿。

Vector Labels有个弊端，就是不能添加动画，而且src设为一张gif的图也没效果.(<span style="font-size: 12px">ps: 也可能是我没找到方法，试过用Vector Labels让mark点动起来的朋友可以告诉我一下.谢谢</span>)
