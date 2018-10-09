---
title: Event 事件对象总结
---

# Event

浏览器事件总结



### Table of contents















### 模拟事件

创建事件对象, 触发事件执行



* **createEventObject**

  创建事件对象

  ```js
  var eventObj = document.createEventObject()
  ```

* **createEvent**

  创建事件对象

  ```js
  var eventObj = document.createEvent('Events')
  ```

* **eventObj.initEvent**

  初始化事件对象类型

  ```js
  if (eventObj.initEvent) {
      eventObj.initEvent('keyup', true, true)
  }
  ```

* **el.dispatchEvent**

  分发事件

  ```js
  document.querySelector('div').dispatchEvent(eventObj)
  ```

* **el.fireEvent**

  分发事件

  ```js
  document.fireEvent('onkeyup', eventObj)
  ```



