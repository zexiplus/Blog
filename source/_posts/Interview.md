---
title: 常用面试问题记录与分析
---

# interview

> 收录了经典前端面试题和解答



### 目录

[TOC]





### 优质网站

- https://blog.csdn.net/kongjiea/article/details/46341575
- https://segmentfault.com/a/1190000000465431
- http://www.cnblogs.com/syfwhu/p/4434132.html



### 术语

#### xss 和 csrf区别

- **csrf (Cross-site request forgery)** 

  跨站请求伪造， 攻击者盗用了你的身份，以你的名义发送恶意请求 。

  条件

  1.登录受信任网站A，并在本地生成Cookie。

  2.在不登出A的情况下，访问危险网站B。

  ![csfr](./imgs/csrf.jpg)

- **xss （Cross-site scripting）**

  * 分类

    1.持久型（永久上传某段代码，之后的所有用户都会被攻击）

    2.非持久型（让某个用户点击恶意代码片段连接，只对这个用户攻击）恶意代码注入，将恶意代码片段通过任何途径上传到服务器端，当下次用户进行访问时就会执行恶意代码

  * 防御

    1.过滤用户输入，谨慎存取
    2.对用户输入进行转码



#### http 和 https 的区别

* http默认端口80，https默认端口443

* https采用ssl加密，http无加密

* https的web服务器启用ssl需要获得一个服务器证书，并将该证书与要使用ssl的服务器绑定



#### 懒加载（load on demand)

懒加载或者按需加载，是一种很好的优化网页或应用的方式。这种方式实际上是先把你的代码在一些逻辑断点处分离开，然后在一些代码块中完成某些操作后，立即引用或即将引用另外一些新的代码块

```js
// 1.webpack 使用promise和async函数实现 懒加载

// 2.vue 使用 import 函数
Vue.component('AsyncCmp', () => import('./AsyncCmp'))

// 3.react 与 vue 类似
const LoadableComponent = Loadable({
  loader: () => import('./Dashboard'),
  loading: Loading,
})

export default class LoadableDashboard extends React.Component {
  render() {
    return <LoadableComponent />;
  }
}

// 图片懒加载 <img> 标签不要设置src属性，放在自定义属性中，根据window.scrollTop判断图片是否出现在用户视野中，如果出现 将自定义属性中的 url 放入src属性中
```



------

#### 浏览器在输入url敲回车后发生了什么

* **步骤**

  1.DNS域名解析；
  2.建立TCP连接；
  3.发送HTTP请求；
  4.服务器处理请求；
  5.返回响应结果；
  6.关闭TCP连接；
  7.浏览器解析HTML；
  8.浏览器布局渲染；


* **步骤详解**
  * **建立tcp连接**

![tcp三次握手](./imgs/tcp.jpg)

​	

* **发送http请求**​	

![http-request](./imgs/http_request.jpg)

* **关闭tcp连接**


![closeLink](./imgs/closeLink.jpg)



* **浏览器解析html**

  浏览器需要加载解析的不仅仅是HTML，还包括CSS、JS。以及还要加载图片、视频等其他媒体资源。

  浏览器通过解析HTML，生成DOM树，解析CSS，生成CSS规则树，然后通过DOM树和CSS规则树生成渲染树。渲染树与DOM树不同，渲染树中并没有head、display为none等不必显示的节点。

  要注意的是，浏览器的解析过程并非是串连进行的，比如在解析CSS的同时，可以继续加载解析HTML，但在解析执行JS脚本时，会停止解析后续HTML，这就会出现阻塞问题。

* **浏览器布局渲染**

根据渲染树布局，计算CSS样式，即每个节点在页面中的大小和位置等几何信息。HTML默认是流式布局的，CSS和js会打破这种布局，改变DOM的外观样式以及大小和位置。这时就要提到两个重要概念：replaint和reflow。

> replaint：屏幕的一部分重画，不影响整体布局，比如某个CSS的背景色变了，但元素的几何尺寸和位置不变。
> reflow： 意味着元件的几何尺寸变了，我们需要重新验证并计算渲染树。是渲染树的一部分或全部发生了变化。这就是Reflow，或是Layout。

所以我们应该尽量减少reflow和replaint，我想这也是为什么现在很少有用table布局的原因之一。

最后浏览器绘制各个节点，将页面展示给用户。



### 高级问题



#### 分析双向数据绑定的原理，并用简单的代码实现

```js

function Vue(options) {
  this.$init(options);
}
Vue.prototype.$init = function(options = {}) {
  let data = this._data = options.data || {}
  let self = this
  let dep = new Dep()
  // 属性代理 vm.a === vm.data.a
  Object.keys(data).forEach((key, index) => {
    Object.defineProperty(self, key, {
      configurable: true,
      enumerable: true,
      get(){
        return data[key]
        dep.depend()
      },
      set(val) {
        data[key] = val
        dep.notice() 
      }
    })
  })
}

function Dep() {
  // 
}
Dep.prototype.notice = function() {
  // 触发页面更新
}
Dep.prototype.depend = function() {
  // 关联当前所有数据和watcher的关系
}

let vm = new Vue({data: {a: 1, b: 2}})


console.log(vm.a === vm._data.a) // 实例访问数据
vm.a = 3
console.log(vm._data.a)
```



#### 手动封装一个promise库，能实现基本的promise api。





#### js实现快速排序（前端常见算法举例说明）



#### 实现深度拷贝

```js
function clone(obj) {
    if (obj instanceof Array) {
        let ret = []
        obj.forEach((item, index) => {
            ret[index] = clone(item)
        })
        return ret
    } else if (obj intanceof Object) {
        let ret = {}
        Object.keys(ret).forEach((item, index) => {
            ret[item] = clone(obj[item])
        })
        return ret
    } else {
        return obj
    }
}
```



### 面试实战

#### 2018.10.13 

* **浏览器小于12px像素字体显示**

  ```css
  span {
      font-size: 12px;
      transform: scale(0.8)
  }
  ```

* **html doctype的意义 (标准模式和兼容模式)**

  标准模式的排版和js以浏览器支持的最高标准运行,  兼容模式浏览器以向后兼容的方式模拟老旧浏览器的行为防止站点无法工作

* **实现ie6, 7 , 8不同字体颜色**

  ```css
  span {
      .color: #ccc\9; /*ie 6,7,8 */
      +color: #000; /* ie 6,7 only  */
      _color: #777; /* ie6 only */
  }
  ```

* **Webpack热刷新原理** 

  使用webpack-hot-middleware插件, 使用SSE(server sent events)服务器事件

  ```js
  // client
  var listener = new EventSource('/message')
  listener.onmessage = function (e) {
      console.log(e.data)
  }
  
  // server
  http.createServer(function (req, res) {
      if (req.url == '/message') {
          res.writeHead(200, {
              'Content-Type': 'text/event-stream',
              'Cache-Control': 'no-cache',
              'Connection': 'keep-alive'
          })
          var i = 0
          setInterval(function() {
              i ++
              res.write('update')
          }, 1000)
      }
  }).listen(3000)
  ```

* **css 实现等边三角形**

  ```css
  .box {
      border-bottom: 1px solid #fff;
      width: 100px;
      height: 100px;
      position: relative;
  }
  
  .box:after, box:before {
      position: absolute;
  }
  .box:before {
      transform: rotate(30deg);
      transform-origin: left bottom;
  }
  .box:after {
      transform: rotate(60deg);
      transform-origin: right bottom;
  }
  ```

* **react组件的生命周期**

  * **实例化**
    - getDefaultProps
    - getInitialState (**此时可以访问this.props**)
    - componentWillMount
    - render
    - componentDidMount
  * **存在期**
    - componentWillReceiveProps
    - shouldComponentUpdate (首次渲染不会调用) 
    - componentWillUpdate
    - componentDidUpdate
  * **销毁&清理期**
    - componentWillUnmount

* **js的继承机制**

  * **原型继承**

  * **类式继承(借用构造函数)**

    ```js
    function Sup() {
        this.name = 'Sup'
    }
    
    function Sub() {
        Sub.call(this)
    }
    ```

  * **混合继承(同时包含原型继承和类式继承)**

  * **实例继承(寄生式继承)**

    ```js
    function Sup() {
        this.name = 'Sup'
    }
    
    function Sub() {
        var obj = new Sup()
        obj.name = 'Sub'
        return obj
    }
    ```

  * **寄生组合式继承**

    ```js
    function Sup() {
        var prototype = Object(superType.prototype)
        prototype.constructor = subType
        subType.prototype = prototype
    }
    ```




#### 2018.10.17



* **防止JS对象被修改**

  * 不可扩展对象Object.preventExtensions(obj) [不能添加新成员]

  * 密封对象 Object.seal(obj) [不能删除, 但属性可修改]

  * 冻结对象 Object.freeze(obj) [不能删不能增不能改]

  * 设置属性 Object.defineProperty, Object.defineProperties

    ```js
    Object.defineProperty(obj, 'name', {
        configurable: boolean, // 是否可删除
        enumerable: boolean, // 是否可枚举
        writable: boolean, // 是否可修改
        value: val // 属性值
    })
    ```



* **CSS选择符有哪些？哪些属性可以继承？**

  可继承 **字体, 颜色, 字大小, 缩进**



* **前端存储方式有哪些？**

  **Cookie, localStorage, sessionStorage, indexDB**

* **什么是面向对象？面向对象有哪些基本特征？**


  * 面向对象是一种思想. 面向对象是指, 把复杂过程封装在对象中,细节交给对象实现, 只暴露出简单的接口,让对象去实现具体的细节.  这种思想将数据作为第一位, 方法其次, 这是对数据的优化, 简化了过程.  通过继承机制, 实现对象之间的属性,方法共用.

  * **封装性**: 隐藏具体细节, 隔离变化, 仅提供外部访问的接口

  * **继承性:** 子类继承父类的一些方法, 可以提高代码复用性

  * **多态性: **同一方法可以在子类和父类有不同实现

* **千位符**

  ```js
  function format(num){
      if(!num) return
      var numString = num.toString()
      var trailIndex = numString.indexOf('.')
      var headString
      if (trailIndex >= 0) {
          var trail = numString.slice(trailIndex)
          headString = numString.slice(0, trailIndex)
          return numString.replace(/(\d{3}\B)/g, function($1) {
              return $1 + ','
          }).concat(trail)
      } else {
  		headString = numString
          return numString.replace(/(\d{3}\B)/g, function($1) {
              return $1 + ','
          })
      }
  }
  
  console.log(format(1231423423.22)) //1,231,423,423.22
  ```


* **快排算法**

  ```js
  var quicksort = function (arr) {
      // 递归函数, 终止情况为数组的长度为1
      if (arr.length <= 1) {
          return arr;
      }
      var pivotIndex = Math.floor(arr.length / 2); // 选取一半位置为基准点
      var pivot = arr.splice(pivotIndex, 1)[0]; // 挑选出基准值
      var left = [];
      var right = [];
      // 建立左右两个数组, 左边存放小于基准的数值, 右边存放大于基准的数值
      for (var i = 0; i < arr.length; i++) {
          if (arr[i] < pivot) {
              left.push(arr[i]);
          } else {
              right.push(arr[i]);
          }
      }
      // 调用自身并进行连接 返回排序后的数组
      return quicksort(left).concat([pivot], quicksort(right));
  };
  var array = [8, 7, 0, 7, 5, 2, 5, 3, 1];
  quicksort(array); // [0,1,2,3,5,5,7,7,8] 
  ```

* **链表与数组的区别**

  * 数组是在内存中连续存放的

  * 插入存储效率低

  * 查找效率高

  * 不利于扩展, 数组定义的空间不够要重新定义数组

  * 链表在内存中存放不是连续的

  * 每一个数据都保存着下一个数据的地址

  * 插入增加数据效率高

  * 查找数据效率低

  * 不指定大小, 扩容方便

* **性能优化**

  * 合并文件 , 使用 css精灵图以 减少http请求

  * 使用合适的缓存策略 响应头增加 expire, max-age字段 增加E-tag

  * 选择适当的图片格式, 压缩图片质量

  * 使用cdn

  * 选择合理的 web component更新方式和周期

  * 压缩组件, js,css

  * 减少重定向

  * 不要使用css表达式

  * 减少dns查询次数

  * 合理使用预加载和懒加载

* **进程间通信(ipc)方式有哪些**

  * 匿名管道(**pipe**) 半双工, 数据单向流动, 只能在亲缘(父子)进程间使用
  * 具名管道(**named pipe**) 允许非亲缘管道间使用
  * 高级管道(**popen**)  将另一个进程在当前程序中启动
  * 消息队列(**message queue**) 消息队列是存放消息的链表, 克服了管道只能传递无格式字节流, 和缓冲区大小受限的情况
  * 信号(**sinal**)
  * 共享内存通信(**shared memory**) 由一个进程创建, 多个进程共享的内存, 是最快的进程间通讯方式
  * 套接字(**socket**)  可用于不同主机之间通讯 步骤 命名, 绑定, 监听, 连接, 发送信息, 解绑



#### 10.18

* **简单与复杂请求**

  * **简单请求**: 两者必须都满足

    * 仅包含GET, HEAD or POST(如果是post, content-type必须是 application/x-www-form-urlencoded, multipart/form-data, or text/plain 其中一种)
    * 没设置自定义头信息的请求 

  * **复杂请求**

    不满足简单请求的请求类型

    1. 获取服务器支持的HTTP请求方法；也是黑客经常使用的方法。
    2. 用来检查服务器的性能。例如：AJAX进行跨域请求时的预检，需要向另外一个域名的资源发送一个HTTP OPTIONS请求头，用以判断实际发送的请求是否安全。

* **http2**

  * **首部压缩**

    * 如果首部发生变化了，那么只需要发送变化了数据在Headers帧里面，新增或修改的首部帧会被追加到“首部表”

  * **共享同一个tcp连接**

    * “资源合并减少请求”的优化手段对于HTTP2.0来说是没有效果的，只会增大无用的工作量而已
    * http1一个域名限制打开6个tcp连接， 所以使用cdn1， cdn2 ， cdn3 ...分发不同资源， http2不需要

  * **并行双向字节流的请求和回应**

    * 同一链接上有多个不同方向的数据流在传输。客户端可以一边乱序发送stream，也可以一边接收者服务器的响应，而服务器那端同理

  * **请求分有优先级**

    * 每个HTTP2.0流里面有个优先值，这个优先值确定着客户端和服务器处理不同的流采取不同的优先级策略，高优先级的流都应该优先发送，但又不会绝对的

  * **服务端推送**

    * 除了对最初请求的响应外，服务器还可以额外向客户端推送资源，而无需客户端明确地请求

    * 下次请求时直接从缓存中读取

* **diff算法**

  * 

* **xss, csrf防范**

* **cookie设置**



#### 10.19



* **讲讲对mvvm模式的理解**

  **model（模型层）， view（视图层）， viewmodel（展示模型)**

  展示模型将模型层中的**数据与复杂的业务逻辑封装成属性与简单的数据**暴露给视图，让视图和展示模型中的属性进行同步, 同时用户改变视图, 视图通过视图模型, 修改数据同步至模型上.



* **讲讲至今遇到的最大困难**

  what，how，why,  done，right，better

* **说一下Event loop**

  **Event Loop是一个程序结构，用于等待和发送消息和事件.**

  简单说，就是在程序中设置两个线程：一个负责程序本身的运行，称为"主线程"；另一个负责主线程与其他进程（主要是各种I/O操作）的通信，被称为"Event Loop线程"（可以译为"消息线程"）

  Node采用的是单线程的处理机制(所有的I/O请求都采用非阻塞的工作方式)，至少从Node.js开发者的角度是这样的。而在底层，Node.js借助libuv来作为抽象封装层，从而屏蔽不同操作系统的差异，Node可以借助livuv来实现线程。

  Libuv库负责将不同的任务分配给不同的线程，形成一个事件循环，以异步的方式将任务的执行结果返回给V8引擎。

  每一个I/O都需要一个回调函数——一旦执行完便堆到事件循环上用于执行

  ![libuv](.\/imgs/libuv.png)

  ![eventloop](./imgs/eventLoop.png)

* **vue-router 的 跳转实现原理**

  我们都知道，单页面应用(SPA)的核心之一是: **更新视图而不重新请求页面**;vue-rouetr在实现单页面前端路由时，提供了两种方式：**Hash模式和History模式；根据mode参数来决定采用哪一种方式**。

  那为什么这两种方式能够实现试图更新不跳转，其原因在于：

  * **Hash模式**： 
    ​ hash（#）是URL 的锚点，代表的是网页中的一个位置，单单改变#后的部分，浏览器只会滚动到相应位置，不会重新加载网页，使用”后退”按钮，就可以回到上一个位置；

    1 $router.push() //显式调用方法

    2 HashHistory.push() //（window.location.hash= XXX）

    3 History.transitionTo() //开始更新

    4 History.updateRoute()  //更新路由

    5 {app._route= route} 

    6 vm.render() //更新视图

    7监听hash变化(**window.onhashchange**)

  * **History模式：** 
    ​    HTML5 History API提供了一种功能，能让开发人员在不刷新整个页面的情况下修改站点的URL，就是利用 **history.pushState** API 来完成 URL 跳转而无须重新加载页面；

    * **history.replaceState**

        仅仅替换浏览器的地址栏, 并不发出请求, 退后按钮无作用

        `history.replaceState(null, null, 'hello');`

    * **history.pushState**

           `history.pushState([data], [title], [url]);`

        点击浏览器的后退按钮，你会发现它和你预想的效果一样。因为pushState方法将我们传给它的URL添加到浏览器的history中，从而改变了浏览器的history,在HTML5History的构造函数中监听popState（**window.onpopstate**）



#### 10.20

* **web前沿技术**
  * rx.js
  * tars.js