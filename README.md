# 微信小程序自定义底部tabbar

 ## 创建tabbar代码文件
 [微信官网tabbar](https://developers.weixin.qq.com/miniprogram/dev/framework/ability/custom-tabbar.html)
 在根目录下创建文件夹`custom-tab-bar`及相关页面
 ```
 custom-tab-bar/index.js
custom-tab-bar/index.json
custom-tab-bar/index.wxml
custom-tab-bar/index.wxss
 ```
`custom-tab-bar`文件下的页面代码可参考官网示例代码

## 配置信息

 - 在`app.json`中的`tabBar`项指定`custom`字段  
 - 与官网不同，我的所有tab页并非component构造器创建而是普通的页面所以不用在每个tab页的`json`里声明`usingComponents`项


```
{
  "pages": [
    "pages/index/index",
    "pages/video/index",
    "pages/mine/index",
    "pages/shop/index"
  ],
  "tabBar": {
    "custom": true,
    "color": "#666",
    "selectedColor": "#E5BA72",
    "borderStyle": "black",
    "backgroundColor": "#ffffff",
    "list": [
      {
        "pagePath": "pages/index/index",
        "iconPath": "static/images/index.png",
        "selectedIconPath": "static/images/index-selected.png",
        "text": "首页"
      },
      {
        "pagePath": "pages/video/index",
        "iconPath": "static/images/bussinessIndex.png",
        "selectedIconPath": "static/images/bussinessIndex-selected.png",
        "text": "视频"
      },
      {
        "pagePath": "pages/shop/index",
        "iconPath": "static/images/shop.png",
        "selectedIconPath": "static/images/shop-selected.png",
        "text": "店铺"
      },
      {
        "pagePath": "pages/mine/index",
        "iconPath": "static/images/mine.png",
        "selectedIconPath": "static/images/mine-selected.png",
        "text": "我的"
      }
    ]
  },
  "window": {
    "backgroundTextStyle": "light",
    "navigationBarBackgroundColor": "#fff",
    "navigationBarTitleText": "WeChat",
    "navigationBarTextStyle": "black"
  },
  "style": "v2",
  "sitemapLocation": "sitemap.json"
}
```
## tab页
>引用官网：自定义组件新增 getTabBar 接口，可获取当前页面下的自定义 tabBar 组件实例。

每个tab页内容在onShow的时候都需要通过`getTabBar`接口设置自定义tabbar里的`selected`值

以`pages/index/index.js`为例：
```
Page({
  onShow() {
    if (typeof this.getTabBar === 'function' &&
      this.getTabBar()) {
      this.getTabBar().setData({
        selected: 0
      })
    }
  }
})
```