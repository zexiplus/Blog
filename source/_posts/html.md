---
title: Html
---

# html

> html总结



### 目录

[TOC]

### html 组件

* **html imports**

  > 状态, 草案
  >
  > 垫片方案   引用google 的 webcomponents.js

  ```shell
  <link rel="imports" href="myFile.html" />
  ```



### html标签



#### meta 关键字

* **viewport**

  > 浏览器视窗大小

  * width = device-width  宽度等于设备宽度
  * Initial-scale=1  初始化大小为1(不缩放)
  * Maxium-scale=1 最大尺寸为1
  * Minium-scale=1 最小尺寸为1

  ```html
  <meta name="viewport" content="width=device-width, initial-scale=1, maxium-scale=1">
  ```

* **description**

  > 网站描述(利于seo)

  ```html
  <meta name="description" content="this is a superme website...">
  ```

* **screen-orientation**

  > 屏幕方向

  * portrait 强制竖向显示

  ```html
  <meta name="screen-orientation" content="portrait">
  ```

* **format-detection** 

  > 文本格式化方案

  * telephone=no 手机号不显示为拨号连接

  ```html
  <meta name="format-detection" content="telephone=no">
  ```

#### a超链接

* **a 标签跳转**

   ```html
   <!-- 相同页面跳转 -->
   <a href="#my-place"></a>
   ...
   <div id="my-place">
       
   </div>
   
   <!-- 不同页面跳转 -->
   <a href="space.html#my-place"></a>
   ```

* **a标签下载**

   ```html
   <a download="file_name" href="file_path">download</a>
   ```

* **a标签target**

   ```html
   <a src="test.html" target="custom-iframe">点击设定iframe链接</a>
   <iframe id="custom-iframe">
       
   </iframe>
   ```

* **取消焦点控制**

  ```html
  <a tabindex="-1" >按tab 焦点不会聚焦到此a标签</a>
  ```


#### **figure**

```html
<figure>
    <figcaption>These words are the caption of the picture. This is called a
        ligature.</figcaption>
    <img src='ligature.svg'/>
</figure>
```

look like this ![figure](/Users/float/Desktop/GitHub/blog/source/_posts/imgs/figure.png)







### Html 模版



#### pug(jade)

> html 模板引擎，可以配合express koa做服务端渲染 

> [pug在线文档](https://pugjs.org/language/attributes.html) 

* **属性**

  ```jade
  a(href='www.bing.com',class='myClass') hello
  //- （）括号内普通属性属性之间空格或逗号, 空格后标签文字
  
  - var flag = true
  span(class=flag ? 'light' : 'dark')
  //- 变量表达式 - 之后
  ```


