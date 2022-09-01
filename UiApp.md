# 注意的坑

>  Swiper组件

```css
组件名称 不能为 Swiper 会有冲突
swiper 本身是由默认高度的
swiper{
	height:400rpx /*修改 swiper 的高度*/ 
}
```



> Page.json 配置

```json
{
    "path": "pages/login/login",
    "style": {
        "navigationBarTitleText": "",
        "enablePullDownRefresh": false,
        "app-plus": {
            "scrollIndicator": "none",   //隐藏滚动条
            "titleNView": false // 页面导航取消
        },
        "disableScroll": true // 禁止页面上下滚动
    }

},
```

