# vscode 提示插件

```shell
cd project
npm install --save @types/cesium
```



# Cesium 开发资源

## 高德开发者 API

```
Key 名称  - Mifan	
Key - 64acf252ea04e90000b43025ad01417d	
安全密钥 - 22152dd0d931b3b0a81bc6528d2e9f6f
```

## 天地图

```
543d7a77ce84c84ef7859f2f8c07f27a
```

## Cesium 官网 Token

```
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJqdGkiOiIyNmEzYjI4ZS01N2U4LTQyYWUtYmRhNS04YTllZmYwMmZjM2EiLCJpZCI6MTAyNjM1LCJpYXQiOjE2NTg4NTEzNzF9.pLFs9Ej-JoR6X-XMKJBRY2TzQ26SDc9dPyDmPxXZ6W8
```

# 开发环境

插件 ( 任务 自己写一个开发插件 )

```
https://github.com/nshen/create-cesium
```





# 快速开始

插件 搭建项目环境

`yarn create cesium`

# 初始化一个球

```js
// 隐藏小部件
animation: false, // 隐藏动画控件
baseLayerPicker: false, // 隐藏图层选择控件
fullscreenButton: false, // 隐藏全屏按钮
vrButton: false, // 隐藏VR按钮，默认false
geocoder: false, // 隐藏地名查找控件
homeButton: false, // 隐藏Home按钮
infoBox: false, // 隐藏点击要素之后显示的信息窗口
sceneModePicker: false, // 隐藏场景模式选择控件
selectionIndicator: true, // 显示实体对象选择框，默认true
timeline: false, // 隐藏时间线控件
navigationHelpButton: false, // 隐藏帮助按钮
scene3DOnly: true, // 每个几何实例将只在3D中呈现，以节省GPU内存
shouldAnimate: true, // 开启动画自动播放
sceneMode: 3, // 初始场景模式 1：2D 2：2D循环 3：3D，默认3
requestRenderMode: true, // 减少Cesium渲染新帧总时间并减少Cesium在应用程序中总体CPU使用率
// 如场景中的元素没有随仿真时间变化，请考虑将设置maximumRenderTimeChange为较高的值，例如Infinity
maximumRenderTimeChange: Infinity,
imageryProvider: tianditu
terrainProvider: new Cesium.createWorldTerrain({
    // 设置地形和水面
    requestWaterMask: true,
    requestVertexNormals: true,
}),
// 出去版本信息
viewer._cesiumWidget._creditContainer.style.display = 'none'
```





# 绘制不同的几何图形

`Entity`   具体请看 http://cesium.xin/wordpress/archives/102.html

```js
let mesh = viewer.entities.add({
    name: "Point",
    position: Cesium.Cartesian3.fromDegrees(118.78, 32.07, 300),
    point: {
        pixelSize: 100,
        color: Cesium.Color.RED
    }
})
// 添加
viewer.zoomTo(viewer.entities)
```











# 相机系统



## setView











# 功能实现

## 水面特效

```js
class WaterPrimitive{
    constructor(positions, options) {
        this.positions = positions;
        this.options = options;
        return this.createPrimitive();
    }

    createPrimitive() {
        //创建水体geometry
        let polygon1 = new Cesium.PolygonGeometry({
            polygonHierarchy: new Cesium.PolygonHierarchy(this.positions),
            perPositionHeight: true,
            vertexFormat: Cesium.EllipsoidSurfaceAppearance.VERTEX_FORMAT
        });

        let primitive = new Cesium.Primitive({
            geometryInstances: new Cesium.GeometryInstance({
                geometry: polygon1
            }),
            appearance: this.getApper(),
            show: true
        });
        return primitive;
    }

    getApper() {
        let apper = new Cesium.EllipsoidSurfaceAppearance({
            aboveGround: true
        });

        apper.material = new Cesium.Material({
            fabric: {
                type: 'Water',
                uniforms: {
                    baseWaterColor: this.options.baseWaterColor,
                    normalMap: this.options.normalMap,
                    frequency: this.options.frequency,
                    animationSpeed: this.options.animationSpeed,
                    amplitude: this.options.amplitude,
                    specularIntensity: this.options.specularIntensity,
                }
            }
        });

        return apper;
    }
}
```









# 遇到的问题

>  深度检测

加载模型定位 移动视角 模型的位置改变

```
this.viewer.scene.globe.depthTestAgainstTerrain = true
```

