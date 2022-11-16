# leaflet

[leaflet官方文档](https://leafletjs.com/)

## 引入leaflet

```bash
<!-- 引入leaflet相关的文件 -->
<link rel="stylesheet"
href="https://unpkg.com/leaflet@1.7.1/dist/leaflet.css"
integrity="sha512-xodZBNTC5n17Xt2atTPuE1HxjVMSvLVW9ocqUKLsCC5CXdbqCmblAshOMAS6/keqq/sMZMZ19scR4PsZChSR7A=="
crossorigin="" />
<script src="https://unpkg.com/leaflet@1.7.1/dist/leaflet.js"
integrity="sha512-XQoYMqMTK8LvdxXYG3nZ448hOEQiglfqkJs1NOQV44cWnUrBc8PkAOcXy20w0vlaXaVUearIOBhiXZ5V3ynxwA=="
crossorigin=""></script>
```

## 右键工具

[Leaflet.contextmenu](https://github.com/aratcliffe/Leaflet.contextmenu)

## 折线

[Leaflet.PolylineDecorator](https://github.com/bbecquet/Leaflet.PolylineDecorator)

使用方法：（直接在html中引入）

```bash
<script src="https://unpkg.com/@geoman-io/leaflet-geoman-free@latest/dist/leaflet-geoman.min.js"></script>
```

* [绘制带箭头的线条（路径）](https://blog.csdn.net/zcylyzhi4/article/details/115317649)
* [带箭头轨迹以及沿轨迹带方向的动态marker](https://www.jianshu.com/p/b38e65101bc2)

## 插件

### Leaflet.markercluster 点聚合

[https://github.com/Leaflet/Leaflet.markercluster/blob/master/README.md](https://github.com/Leaflet/Leaflet.markercluster/blob/master/README.md)

 [Leaflet.markercluster  中文文档](https://blog.csdn.net/SuiFengDieWu/article/details/125886094)

 ### L.TileLayer.Colorizr 地图图层颜色

 [L.TileLayer.Colorizr](https://github.com/hnrchrdl/leaflet-tilelayer-colorizr/blob/master/README.md)

缺点：使用之后加载明显变卡顿。

 ```bash
this.layers = L.tileLayer.colorizr('//webrd0{s}.is.autonavi.com/appmaptile?lang=zh_cn&size=1&scale=1&style=8&x={x}&y={y}&z={z}', {
    maxZoom: 18,
    attribution: "高德地图 AutoNavi.com",
    subdomains: "1234",
    colorize: (pixel) => {
    	// 这个方法用来调整所有的图片上的rgb值，pixel是图片原有的rgb值
        pixel.r += 13;
    	pixel.g += 17;
    	pixel.b += 90;
    	return pixel
    }
}).addTo(this.myMap);
 ```

## 一些优化方案

### 如何加载10万数据

* [掘金-加载10完数据](https://juejin.cn/post/6844904199709278221)


## problems

1.共用id的地图，在遇到tab切换时，会出现只展示一小块地图的情况。

解决：`this.leafletMap.invalidateSize(true);`