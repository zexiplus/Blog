# vue源码解读学习笔记

学习vue源码解读课程的一些笔记



## 目录

[TOC]



### vue项目准备

#### 类型检查

vue使用flow做静态类型检查, 包括

* 类型推断

  ```js
  /*@flow*/
  function add(x: number, y: number): number {
      return x + y
  }
  add('123', 123)
  ```

* 类型注释



#### 构建

* Runtime only 

  在构建时编译, 也叫离线编译,通过webpack,vue-loader等工具编译出能直接使用的js代码.  编译比较耗费性能, 推荐使用构建时编译, 在使用render函数时可使用此选项, 例如

  ```js
  new Vue({
      render(h) {
          return h('div', this.data)
      }
  })
  ```

* runtime + complier

  运行时编译, 使用包含构建功能的vuejs, 在使用template时需要使用运行时编译选项, 例如:

  ```js
  new Vue({
      template: '<div>{{data}}</div>'
  })
  ```



### 数据驱动

#### vue init 初始化

* new Vue(options) 发生了什么?
  * 对options进行合并
  * 执行了一系例初始化方法, initLifecycle, initEvents, initRender, initState等
  * 将data代理到this对象上(proxy)
  * 对数据进行响应式处理
  * mount挂载

* **调试技巧**

  在vue.esm.js中**_init**方法增加debugger, 查看vue初始化时的变量



#### vue mount 挂载

