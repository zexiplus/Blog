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



## 问答

#### 什么是AST？

AST（abstruct syntax tree）抽象语法树， 是源代码的抽象结构的树状表现。

Vue在mount过程中， template会被编译为AST，经过generate（AST转化为render函数）得到render， render函数返回Vnode， Vnode是Vue的虚拟dom节点， 保存着标签名， 子节点， 属性， 文本信息等







## 章节



#### 2-1 数据驱动

vuejs核心思想之一就是数据驱动. 是指视图是由数据驱动, 对视图的修改不会直接操作dom, 而是修改数据.

```html
<div>{{message}}</div>
```





#### 2-2 new Vue发生了什么

* 调试vue, 可以在项目的node_modules/vue/dist/vue.esm.js, 中**Vue.prototype._init里增加debugger**
* 发生了什么?
  * **Vue.prototype._init** ---> **initState-->** **initData && observe**  ---> **proxy**
    * **proxy**: 把data代理到vm对象上
    * **observe **: 数据监察

#### 2-3 vue实例挂载实现 $mount

* vue会把template, 或空template, 或用户手写render函数最终都转化为render函数运行输出

#### 2-4 render

* render生成一个Vnode

  ```js
  new Vue({
      el: '#app',
      render(createElement) {
          return createElement('div', {
          	attrs: {
              	id: 'app1'
              }
          }, this.message)
      }, 
      data() {
      	message: 'hello, world'
      }
  })
  ```



#### 2-5 virtual DOM

* virtual dom指的是用一个原生的javascript描述dom节点
* vue使用snabbdom开源库改造实现virtual dom



#### 2-6 createElement

* Vue 使用createElemtent 生成 Vnode



#### 2-7 update

* _update 是vue实例的私有方法, 它调用的时机有两个, 一个是首次渲染, 一个是数据更新的时候.
* _update的作用是把VNode渲染成真实的DOM, 它定义在`src/core/instance/lifesycle.js`中: 