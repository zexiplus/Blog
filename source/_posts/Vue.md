---
title: vue 使用备考指南 
---

# vue

vue 使用,备考指南



## 目录

[TOC]

### vue 构建命令

* 初始化项目

  ```shell
  npm list
  npm init webpack
  ```

* 开发环境运行

  ```shell
  npm run dev
  ```

* 编译并生成报告

  ```shell
  npm run build --report
  ```




### 工程目录结构

* build 文件夹：用于存放 webpack 相关配置和脚本。其中webpack.base.conf.js 用于配置 less、sass等css预编译库

* config 文件夹：主要存放配置文件，用于区分开发环境、线上环境的不同。 其中index.js 配置开发环境的 端口号、是否开启热加载 或者 设置生产环境的静态资源相对路径、是否开启gzip压缩、npm run build 命令打包生成静态资源的名称和路径等。

* dist 文件夹：默认 npm run build 命令打包生成的静态资源文件，用于生产部署。
* static 文件夹, 存放不通过打包的静态资源例如js， 图片等

* node_modules：存放npm命令下载的开发环境和生产环境的依赖包。

* src: 存放项目源码及需要引用的资源文件。
  * src下assets：存放项目中需要用到的资源文件，css、js、images等。

  * src下componets：存放vue开发中一些公共组件：header.vue、footer.vue等。

  * src下emit：自己配置的vue集中式事件管理机制。
  * src下的 const目录： 存放开发环境下的全局常量
  * src下的 filter 目录： 存放自定义过滤器

  * src下router：vue-router vue路由的配置文件。

  * src下service：自己配置的vue请求后台接口方法。

  * src下page：存在vue页面组件的文件夹。

  * src下util：存放vue开发过程中一些公共的.js方法。

  * src下vuex：存放 vuex 为vue专门开发的状态管理器。

  * src下app.vue：使用标签`<route-view></router-view>`渲染整个工程的.vue组件。

  * src下main.js：vue-cli工程的入口文件。

* index.html：设置项目的一些meta头信息和提供`<div id="app"></div>`用于挂载 vue 节点。

* package.json：用于 node_modules资源部 和 启动、打包项目的 npm 命令管理。



### 核心问题解读

#### vue 相关知识

* **vue核心是什么?**

  **双向数据绑定**和**组件系统**

* 怎么理解vue是一套构建用户界面的**渐进式web框架**?

  vue是非侵入式的, 没有多做职责之外的事, vue只提供了双向数据绑定和组件系统, 其他功能由vue插件提供

  体现在:

  * 在原有系统上中某个页面使用vue, 也可以从0开发整个项目

* vue常见的**指令**?

  * v-if, v-show, v-model, v-bind, v-for, v-once
  * v-pre 跳过这个元素和其子元素的编译过程, 用于没有使用vue指令的节点, 加速编译过程

* vue常见的**修饰符**?

  * **v-on事件**常用修饰符

    * .stop停止冒泡, .prevent阻止默认行为, .capture使用捕获模式, .once只触发一次

    * .self只在绑定元素上使用

    * **.native** 监听组件**根元素的原生事件**

      例如在第三方UI组件上绑定事件不起作用, 则使用此修饰符

      ```html
      <el-input @keyup.enter.native="submit"></el-input>
      ```

    * .[keyCode] 只在指定键值码触发

    * .left, .right, .middle 在鼠标左键, 右键, 中键触发

  * **v-model**常用修饰符

    * .number将输入字符串转化为数字

    * .trim去掉首位空格

      ```html
      <input v-model.number="age" />
      ```

  * **v-bind**常用修饰符

    * .sync 会扩展成一个更新父组件绑定值的 v-on 侦听器

    * .prop - 被用于绑定 DOM 属性

      ```html
      <text-document :title.prop="title" ></text-document>
      ```

* v-on可以监听多个方法吗?

  可以, 但是同一种监听器只能响应一个函数, click只能响应一个

  ```html
  <button @focus="handleFocus" @click="handleFocus1" @click="handleFocus2"></button>
  ```



* **key的作用**?

  **用于管理可复用的元素, vue保证高效的渲染元素**, 通常会复用已有元素而不是从头开始.



* **keep-alive 的作用?**

  主要用于**保留组件状态**和**避免重新渲染**, 属性: **include**(保存组件状态)和**exclude**(不缓存组件的状态)

  ```html
  <keep-alive :include="/a|b/" :exclude="['c', 'd']">
      <component :is="viewname">
      </component>
  </keep-alive>
  ```

* **如何编写可复用组件?**

  Props, 事件, slot

  * props 允许外部环境传递变量到内部
  * 事件 允许内部触发外部的行为
  * slot 允许外部环境将内容插入到内部的视图结构



* **vue的生命周期?**

  vue的实例从新建到销毁的过程, 具体包括:

  **开始创建--初始化数据--编译模版--挂载dom渲染--更新渲染—卸载**



* **vue生命周期的钩子函数有哪些， 做了什么？**
  * **beforeCreate** 在`实例初始化之后`，数据观测 (data observer) 和 event/watcher 事件配置之前被调用
  * **created** 在`实例创建完成后`被立即调用。在这一步，实例已完成以下的配置：`数据观测 (data observer)`， `属性和方法的运算`，`watch/event 事件回调`, 此时$el属性未赋值，ajax调用建议在此阶段执行
  * **beforeMount**  在`挂载开始之前`被调用：相关的 render 函数首次被调用
  * **mounted** `el` 被新创建的 `vm.$el` 替换，并`挂载到实例上去之后`调用该钩子
  * **beforeUpdate**`数据更新时调用`，发生在虚拟 DOM 打补丁之前。这里适合在更新之前访问现有的 DOM
  * **updated** 由于数据更改导致的`虚拟 DOM 重新渲染和打补丁`，在这`之后`会`调用`该钩子
  * **activated** keep-alive 组件激活时调用
  * **deactivated** keep-alive 组件停用时调用
  * **beforeDestroy** 实例销毁之前调用。在这一步，实例仍然完全可用
  * **destoryed** Vue 实例销毁后调用
  * **errorCaptured** 当捕获一个来自子孙组件的错误时被调用。此钩子会收到三个参数：错误对象、发生错误的组件实例以及错误信息字符串




