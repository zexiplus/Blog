---
title: 常用js技巧片段
---



# JS-TIPS



* **解析字符串为表达式的方法**

  * eval("" + expr + "")

  * new Function()

    ```js
    let fn = new Function('item', 'return item + 1')
    fn(5)
    ```

* 

