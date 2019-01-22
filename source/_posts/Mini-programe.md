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



### API 功能

#### 设置数据

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



#### 列表渲染

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
<!-- content.wxml -->
<block wx:for="{{contentList}}" wx:item="item" wx:key="index" wx:index="index">
  <view>
    <text>{{item.id}}</text>
    <text>{{item.name}}</text>
  </view>
</block>
```



#### 事件绑定

* **事件名:** tap 

  * 绑定触控事件(冒泡): bindtap
  * 绑定触碰事件(不冒泡): catchtap

  ```html
  <text bindtap="onTap"></text>
  <text catchtap="onTap"></text>
  <script>
  	Page({
          onTap: function() {}
      })
  </script>
  ```



#### 路由跳转

* **跳转到子页面(有返回按钮)** `wx.navigateTo()`, 会触发Hide事件

  ```js
  wx.navigateTo({
  	url: "../posts/posts",
      success,
      fail,
      complete
  });
  ```

* **跳转到平级页面(没有返回按钮)** `wx.redirectTo`, 会触发Unload事件

  ```js
  wx.redirectTo({
      url: '',
      success,
      fail,
      complete
  })
  ```

* **跳转传参**

  ```js
  // 索引页面
  wx.navigateTo({
      url: '../posts/posts?id=123"
  })
  
  // 跳转页面
  Page({
      onLoad(options) {
          console.log(options.id) // 123
      }
  })
  ```

  


#### 文件引用与导出

```js
// export.js
module.exports = {
    a: [1, 2, 3]
}

// import.js
var a = reuqire('../url').a

```



#### template模版

* **模版定义**

  name定义模版名

  ```html
  <template name="postItem">
      <view></view>
  </template>
  ```

* **模版引入**

  src指定模版路径

  ```html
  <import src="./post-item/post-item-template.wxml"></import>
  ```

* **模版使用**

  `is`指定使用的模版名, `data` 指定传入的数据

  ```html
  <template is="postItem" data="{{item}}">
  	
  </template>
  ```



#### 样式引用

```css
@import "../abc.wxss";
```



#### 自定义属性

```html
<view catchtap="handleTap" data-post-id="{{item.postId}}"></view>
```

```js
handleTap(event) {
    let id = event.currentTarget.dataset.postId
}
```



#### 数据缓存

> 注意: 小程序缓存最多10mb

```js
// 设置缓存
wx.setStorage({
	key: 'game',
	data: 'overwatch'
})

// 同步获取缓存
var game = wx.getStorageSync('game')

// 异步获取缓存
wx.getStorage({
    key: 'key',
    success(res){
        console.log(res.data)
    }
})

// 清除缓存
wx.removeStorageSync('game')
```



#### 页面提示

**wx.showToast(自动隐藏)**

```js
wx.showToast({
    title: 'hello world',
    duration: 2000,
    icon: 'success'
})
```

**wx.showModal(不自动隐藏, 需要用户确认)**

```js
wx.showModal({
	title: 'hello world',
    content: 'hello world',
    showCancel: true,
    
})
```

**wx.showActionSheet**

```js
wx.showActionSheet({
	itemList: [
        '分享到微信好友',
        '分享到朋友圈',
    ]
})
```



#### 音乐播放

**wx.getBackgroundAudioManager**

> 获得音乐播放器全局实例, 注意: dataUrl, coverImgUrl只能用网络文件不能用本地文件

```js
var audio = wx.getBackgroundAudioManager()
backgroundAudioManager.title = '此时此刻'
backgroundAudioManager.coverImgUrl = ''
// 设置了 src 之后会自动播放
backgroundAudioManager.src = ''
```



**audio.play**

> 播放音频

```js
audio.play()
```

**wx.pauseBackgroundAudio**

> 暂停音频

```js
audio.pause()
```

**audio.onPlay**

> 监听音乐播放

```js
var audio = wx.getBackgroundAudioManager()
audio.onPlay(function(event) {

})
```



#### 全局变量

在小程序打开期间一直存在

```js
// app.js
App({
    globalData: {
        isPlaying: false
    }
})

// otherPage.js
var app = getApp()
Page({
    onLoad() {
        var isPlaying = app.globalData.isPlaying
    }
})

```



#### 动态设置导航条

**wx.setNavigationBarTitle() **

```js
Page({
    onReady() {
        wx.setNavigationBarTitle({
            title: 'title'
        })
    }
}
```







#### 选项卡

> 注意: list 中的pagePath 必须在 pages 中注册过

app.json

```json
{
    ...
    "tabBar": {
       	"list": [
            {
            	"pagePath": "/pages/movie/movie",
                "text": "movie",
                "iconPath": "/images/movie.png",
                "selectedIconPath": "/images/movie-selected.png"
            },
            {
            	"pagePath": "/pages/posts/post",
                "text": "post",
                "iconPath": "/images/post.png",
                "selectedIconPath": "/images/post-selected.png"
            }
        ]
```



#### 请求

**wx.request()**

```js
wx.request({
	url: 'url',
    method: 'GET',
    data: {},
    header: {
    	'Content-Type': 'application/json'
    },
    success() {
    },
    fail() {
    },
    complete() {
    }
})
```





### 知识点

* 只有被`<text>`包裹的文字才可以长按选中, 需要增加selectable属性
* wxml内部最外层元素为`<page>`, 可以通过设置page的背景色(占满全屏)
* 在水平方向用rpx相对单位, 在垂直方向用绝对单位px, 因为手机在水平方向上宽度有限, 在垂直方向上可以滚动



