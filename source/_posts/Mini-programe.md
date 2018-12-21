---
title: 微信小程序学习总结
---

# 微信小程序

### 目录

[TOC]

### 项目结构

```markdown
imgs/
data/ 
utils/
pages/
app.js
app.json
app.wxss
project.config.json
```



### 文件配置

`app.json`  小程序的所有配置项， [详情](https://developers.weixin.qq.com/miniprogram/dev/framework/config.html#%E5%85%A8%E5%B1%80%E9%85%8D%E7%BD%AE)

```json
{
  "pages": [
    "pages/index/index",
    "pages/logs/logs",
    "pages/content/content"
  ],
  "window": {
    "backgroundTextStyle": "light", // 下拉loading的样式
    "navigationBarBackgroundColor": "#fff", // 顶部导航背景色
    "navigationBarTitleText": "WeChat", // 小程序标题
    "navigationBarTextStyle": "black" // 小程序导航文字颜色
  },
  // 底部导航栏配置
  "tabBar": {
    "list": [{
      "pagePath": "pages/index/index", // 导航路径
      "text": "首页",
      "iconPath": "imgs/batman.png", // 导航图标路径
      "selectedIconPath": "imgs/batman.png" // 被选中的导航图片路径
    },
    {
      "pagePath": "pages/content/content",
      "text": "内容",
      "iconPath": "imgs/dare-devil.png",
      "selectedIconPath": "imgs/dare-devil.png"
    }]
  }
}
```



### 方法



#### setData

设置数据

##### 计算器demo

```js
// caculate.js
Page({
    data: {
        input1: 0,
        input2: 0,
        result: 0
    },
   inputa: function (e) {
    this.setData({
      input1: e.detail.value
    })
  },
  inputb: function (e) {
    this.setData({
      input2: e.detail.value
    })
  },
  sum: function () {
    let res = Number(this.data.input1) + Number(this.data.input2)
    this.setData({
      result: res
    })
  },
})
```

```html
<!-- caculate.wxml -->
<input bindInput="inputa"></input>
<text>+</text>
<input bindInput="inputb"></input>
<button bindTap="sum">=</button>
<text>{{result}}</text>
```



#### wx:for

列表渲染

```js
// data/list.js
const contentList = [
    {id: 1, name: '23434'},
    {id: 2, name: '23434'},
    {id: 3, name: '23434'},
]

module.exports = {
    contentList
}
```

```js
// content.js
const contentList = require('../../data/list.js').contentList

Page({
    data: {},
    onLoad() {
        this.setData({
            contentList: contentList
        })
    }
})
```

```html
// content.wxml
<block wx:for="{{contentList}}" wx:key="item">
  <view>
    <text>{{item.id}}</text>
    <text>{{item.name}}</text>
  </view>
</block>
```





