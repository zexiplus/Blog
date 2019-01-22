---
title: 读书笔记
---

# Read Mark

读书笔记



## book list

* 《高效前端： web高效编程与优化实践》
* 







### 高效前端： web高效编程与优化实践



#### 23 节 web 存储

##### web sql(关系型)

Web SQL 是 前端 的 数据库， 它 也是 本地 存储 的 一种， 使用 SQLite 实现， SQLite 是 一种 轻量级 数据库， 它 占用 的 空间 小， 支持 创建 表， 插入、 修改、 删除 表格 数据， 但是 不支持 修改 表 结构， 如 删掉 一 纵列， 修改 表头 字段 名 等， 不过 可以 把 整 张 表 删 了。

* 创建数据库

  ```js
  var db = window.openDatabase('dbname', '1.0', 'db description', 2 * 1024 * 1024)
  // 参数 数据库名， 版本号， 数据库描述， 数据库大小（b）
  ```

* 创建表

  ```js
  db.transaction(function(tx) {
    tx.executeSql(
      "create table if not exists order_ data(order_id primary key, format_city, lat, lng, price, create_time)", // 执行的sql语句
      [], // 选项
      null, // success callback
      function(tx, err) { // error callback
        throw ` execute sql failed: ${err.code} ${err.message}`;
      }
    );
  });
  ```

* 插值

  ```js
  var order = { 
      orderId: 100314, 
      format_city: "New York, NY, USA", 
      lat: 40. 7127837, 
      lng: -74. 0059413, 
      price: 150, 
      createTime: 1473884040000 
  };
  
  tx. executeSql(` insert into order_ data values(${ order. orderId}, '${order. format_ city}', ${ order. lat}, ${ order. lng}, ${ order. price}, '${date}')`);
  ```



##### indexDB(非关系型)

* 创建打开数据库

  ```js
  var request = window. indexedDB. open(" orders", 7);
  request. onsuccess = function( event){ 
      var db = event. target. result;
  }
  
  ```



#### 16节 pwa离线应用

**注册service worker**

```js
window.onload = function () {
    navigator.serviceWorker.register('/sw.js').then(res => {
        
    }).catch(e => {
        
    })
}
```



**离线消息推送**

```js
if (window.pushManager) {
    ... // 支持离线消息推送
}
```



**Web App Manifest 添加 桌面 入口**
