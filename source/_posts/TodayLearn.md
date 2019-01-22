---
title: 整理每日所学的琐碎知识点
---



# Today learnt

按时间线整理知识点, 利于复习和记忆



## 2018



### 10.9

* document.activeElement  访问正在聚焦、高亮的元素
* el.focus()   el.blur()   元素获得失去焦点
* 使普通元素能获得焦点 `<div tabindex="1">enable focus</div>`
* 使表单元素失去焦点 `<input tabindex="-1" />`



### 12.7

* 正则表达式 反向引用 \n, n为数字

  ```js
  var reg = /([a-z]+)(-\1)*/ // 匹配abc-abc-abc ...
  ```

* reg.flags, reg.global为只读属性， 更改无效

  ```js
  reg.flags // ''
  reg.global // false
  ```

* 在元素上同时绑定click和touchstart事件在移动设备会执行两次

  **解决方案**: 在touchstart事件中调用 event.preventDefault()