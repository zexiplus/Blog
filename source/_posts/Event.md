---
title: Event 事件对象总结
---

# Event

浏览器事件总结



### Table of contents









### Event 事件对象

#### 常用属性

* **type**

  > 事件类型 例如 **keydown**

* **键码相关**

  > key, code, which, keyCode

  ```js
  // 例如按键向上箭头事件
  {
  	key: 'ArrowUp',
      code: 'ArrowUp',
  	keyCode: 38,
      which: 38,
  }
  ```

* 



### 模拟事件

创建事件对象, 触发事件执行



* **创建事件对象**

  new Event() || createEventObject || createEvent

  ```js
  var eventObj = new Event('click', {bubbles: false, cancelable: false, composed: false})
  var eventObj1 = document.createEventObject()
  var eventObj2 = document.createEvent('Events')
  var eventobj3 = document.createEvent('KeyboardEvents')
  ```

* **初始化事件对象类型**

  eventObj.initEvent

  ```js
  if (eventObj2.initEvent) {
      eventObj2.initEvent('keyup', true, true)
      eventObj3.initEvent('keydown', true, true, window, "U+0009") // 模拟tab按键
  }
  
  ```

* **分发事件**

  el.dispatchEvent || el.fireEvent

  ```js
  document.querySelector('div').dispatchEvent(eventObj)
  document.fireEvent('onkeyup', eventObj)
  ```


### 焦点事件

* **获得页面当前焦点元素**

  ```js
  document.activeElement
  // 点击焦点按钮
  document.activeElement.click()
  ```

* **获得焦点**

  ```js
  element.focus()
  ```

* **取消焦点**

  ```js
  element.blur()
  ```

* **避免获得焦点**

  ```html
  <a tabindex="-1"></a>
  ```



### 跨域

* **event: message**

  ```js
  window.addEventListener('message', function (e) {
      if (event.origin.indexOf('http://yoursite.com')) {
          // do some thing
      }
  })
  
  ```

* **postMessage**

  ```js
  var frame = document.getElementById('frame')
  frame.contentWindow.postMessage('any thing')
  ```

* **非跨域访问**

  cross-origin 判定规则 `<protocol>://<hostname>:<port>/path/to/page.html` 中protocol, hostname, port 任一不同, 即判定为跨域



  ```js
  // sub page
  function say() {
      alert('hello')
  }
  
  // parent page
  frame.window.say()
  ```
