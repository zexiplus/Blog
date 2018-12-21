---
title: 浏览器兼容性问题
---



# compatible

浏览器兼容问题解决方法



## 目录

[TOC]

## 内容



### html meta

* http-equiv 在多核浏览器（360）中强制使用 IE9渲染引擎渲染

  ```html
  <meta http-equiv="X-UA-Compatible" content="IE=9">
  ```

* 在多核浏览器使用IE最新（本机已安装）的渲染引擎渲染, 如果IE有安装Google Chrome Frame，那么就走安装的组件

  ```html
  <meta http-equiv="X-UA-Compatible" content="IE=Edge,chrome=1" >
  ```


### IE css hack

* `display: inline-block` 在 IE8以下无法正确显示 （只能设置宽高， 无法在一排）

  解决方法： 在`display: inline-block`元素的类上 再次声明 `*display: inline`, 在这里 * 代表 IE 6，7 能识别， _ 代表 IE 6 识别

  ```css
  .block {
      display: inline-block;
  }
  .block {
      *display: inline; /* IE6,7 */
      _display: inline; /* only IE6 */
  }
  ```
