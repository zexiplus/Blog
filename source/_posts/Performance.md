---
title: Web 性能分析
---

# Web performance



### Question 

> 常见问题



#### 尾递归优化

函数调用自身，称为递归。如果尾调用自身，就称为尾递归。

递归非常耗费内存，因为需要同时保存成千上百个调用记录，很容易发生"栈溢出"错误（stack overflow）。但对于尾递归来说，由于**只存在一个调用记录**，所以永远不会发生"栈溢出"错误



```js
// 优化前， 普通递归调用
function factorial(n) {
  if (n === 1) return 1;
  return n * factorial(n - 1);
}

factorial(5) // 120

// 优化后， 尾递归调用
function factorial(n, total) {
  if (n === 1) return total;
  return factorial(n - 1, n * total);
}

factorial(5, 1) // 120
```





#### 什么是阻塞？

在页面中我们通常会引用外部文件，而浏览器在解析HTML页面是**从上到下依次解析**、渲染，如果<head>中引用了一个a.js文件，而这个文件很大或者有问题，需要2秒加载，那么浏览器会停止渲染页面（此时是白屏显示），2秒后加载完成才会继续渲染，这个就是阻塞。



#### 为什么会阻塞？

因为浏览器不知道a.js中执行了哪些脚本，会对页面造成什么影响，所以浏览器会等**js文件下载并执行完成后**才继续渲染，如果这个时间过长，会白屏。

 CSS文件也一样，因为CSS文件会对DOM的样式，布局，色彩，效果产生影响，所以浏览器会等**CSS文件下载并执行完成后**继续。



#### css 阻塞

css 的加载**不会**阻塞dom的解析(DOM tree), 但**会**阻塞dom 树的渲染(render tree). **会**阻塞之后js代码的执行.

为了避免dom树重新渲染回溯影响性能浪费,  所以css代码的加载会阻塞dom树渲染.



#### 加载事件

> load 事件和 DOMContentLoaded 事件

**load事件**: 页面中的所有静态资源加载完成时触发包括样式表, 图像, 脚本

**DOMContentLoaded事件**: 当初始的 **HTML** 文档被完全加载和解析完成之后，**DOMContentLoaded** 事件被触发，而无需等待样式表、图像和子框架的完成加载. **注意**：**DOMContentLoaded** 事件必须等待其所属script**之前**的样式表加载解析完成才会触发



#### 解决阻塞

1. **延迟加载 defer**

   把script标签放到 body 的最后一行,  或者在script标签加入 defer属性

   ```html
   <head>
       <script	src="js/defer.js" defer></script>
       <script	src="js/defer2.js" defer></script>
   </head>
   
   <!-- other -->
   <html>   
   	<body>
   	</body>
   	<script src="js/defer.js"></script>
   </html>
   ```

2. **异步加载 async**

   告知浏览器可以边下载边渲染而不用等到js下载再执行后才渲染, 使用了 async 属性的脚本不能保证执行的先后顺序, 异步脚本一定会在页面**load事件前执行**(所有资源都下载完), 但可能会在**DOMContentLoaded 事件前或后**执行

   ```html
   <head>
       <script src="js/async.js" async></script>
       <script src="js/async2.js" async></script>
   </head>
   ```

   **这两种的不同点**:  

   defer 会 **立即下载**,但到 浏览器解析至html标签时才**顺序执行**.而放在body后的script代码会在遇到这个标签时才下载,下载完成后执行.

3. **动态加载 createElement('script')**

   当有需要时,再加载脚本

   ```js
   function createScript(src) {
       var script = document.createElement('script')
       script.type = 'text/javascript'
       script.src = src
       document.head.appendChild(script)
   }
   document.querySelector('button').onclick = createScript
   ```

4. **load 事件之后加载**

   Onload 事件为页面中所有的图片, 视频,js文件,css文件 等资源都加载完才触发

   ```js
   window.onload = function () {
       createScript('js/onload.js')
   }
   ```

5. **DOMContentLoaded 事件之后加载**

   DOMContentLoaded 事件为 形成完整的DOM树后就会触发, 不会理会图像, javascript文件, css文件等其他资源时候下载完毕

   ```js
   window.addEventListener('DOMContentLoaded', function () {
       createScript('js/onDOM.js')
   })
   ```






### page optmize proposal

网页性能优化的34条建议



1. **Minimize HTTP Requests ** 最小化http请求数

2. **Use a Content Delivery Network** 使用内容分发网络

3. **Add an Expires or a Cache-Control Header** 给相应头增加过期字段

4. **Gzip Components** 压缩组件

5. **Put Stylesheets at the Top** 在head内使用样式表

6. **Put Scripts at the Bottom** 在body的最后一行引入脚本(或增加defer属性)

7. **Avoid CSS Expressions** 

   避免css表达式(只有ie支持css表达式例如top:expression(eval(document.documentElement.scrollTop + document.documentElement.clientHeight - 60)));)

8. **Make JavaScript and CSS External** 确保脚本和样式表是外联文件

9. **Reduce DNS Lookups** 减少dns查询次数

10. **Minify JavaScript and CSS** 最小化js和css

11. **Avoid Redirects** 避免重定向

12. **Remove Duplicate Scripts** 删除重复的脚本

13. **Configure ETags** 相应头配置ETags字段, 从而判断版本信息

14. **Make Ajax Cacheable** 使ajax请求响应可缓存

15. **Flush the Buffer Early** 如果请求事件过长, 先发送部分数据

16. **Use GET for AJAX Requests** 尽可能在ajax请求使用get方法

17. **Post-load Components**  使用延迟加载(对于非必须的优化脚本例如动画,拖动等可以使用延迟加载技术确保主要功能是快速响应的)

18. **Preload Components** 使用预加载(下一页的图片等资源)

19. **Reduce the Number of DOM Elements** 减少dom元素数, 减少嵌套标签,减少空标签

20. **Split Components Across Domains** 拆分组件至不同域来使用同时下载

21. **Minimize the Number of iframes** 使用最少数的iframes

22. **No 404s** http相应是昂贵的, 消除不必要的404响应

23. **Reduce Cookie Size ** 减少cookie大小

24. **Use Cookie-free Domains for Components** 对于静态资源的请求不使用cookie携带

25. **Minimize DOM Access ** 减少dom树的直接操作(缓存已放翁过的元素, 减少页面重构次数)

26. **Develop Smart Event Handlers** 使用高性能的事件处理函数(事件代理, DOMContentLoaded)

27. **Choose <link> over @import** (IE浏览器使用@import引入的css会在页面最下方引入css一样效果)

28. **Optimize Images** 优化图片格式,大小

29. **Optimize CSS Sprites** 优化精灵图

30. **Don't Scale Images in HTML** 图片的尺寸与显示尺寸对应

31. **Make favicon.ico Small and Cacheable** 使网页标题图表小且可缓存

32. **Keep Components under 25K** 使文件小于25k(iphone不会缓存25k以上文件大小)

33. **Pack Components into a Multipart Document** 将文件打包到多个文档

34. **Avoid Empty Image src** 避免图片带有空src属性(减少不必要的请求)





### performance API



#### window.performance

页面性能对象



* **window.performance.timing**

  页面性能时间对象

  >通过`window.performance.timing`所获的的页面渲染所相关的数据，在单页应用中改变了url但不刷新页面的情况下是不会更新的。因此如果仅仅通过该api是无法获得每一个子路由所对应的页面渲染的时间。如果需要上报切换路由情况下每一个子页面重新render的时间，需要自定义上报

  ```js
  let times = {};
    let t = window.performance.timing;
    
    //重定向时间
    times.redirectTime = t.redirectEnd - t.redirectStart;
    
    //dns查询耗时
    times.dnsTime = t.domainLookupEnd - t.domainLookupStart;
    
    //TTFB 读取页面第一个字节的时间
    times.ttfbTime = t.responseStart - t.navigationStart;
    
    //DNS 缓存时间
    times.appcacheTime = t.domainLookupStart - t.fetchStart;
    
    //卸载页面的时间
    times.unloadTime = t.unloadEventEnd - t.unloadEventStart;
    
    //tcp连接耗时
    times.tcpTime = t.connectEnd - t.connectStart;
    
    //request请求耗时
    times.reqTime = t.responseEnd - t.responseStart;
    
    //解析dom树耗时
    times.analysisTime = t.domComplete - t.domInteractive;
    
    //白屏时间
    times.blankTime = t.domLoading - t.fetchStart;
    
    //domReadyTime
    times.domReadyTime = t.domContentLoadedEventEnd - t.fetchStart;
  ```

* **window.performance.getEntries()**

  可以通过window.performance.getEntries()来获取资源的加载和请求相关的数据

  > 通过window.performance.getEntries()所获取的资源加载和异步请求所相关的数据，在页面切换路由的时候会重新的计算，可以实现自动的上报

  ```js
    let  entryTimesList = [];
    let entryList = window.performance.getEntries();
    entryList.forEach((item,index)=>{
    
       let templeObj = {};
       
       let usefulType = ['navigation','script','css','fetch','xmlhttprequest','link','img'];
       if(usefulType.indexOf(item.initiatorType)>-1){
         templeObj.name = item.name;
         
         templeObj.nextHopProtocol = item.nextHopProtocol;
        
         //dns查询耗时
         templeObj.dnsTime = item.domainLookupEnd - item.domainLookupStart;
  
         //tcp链接耗时
         templeObj.tcpTime = item.connectEnd - item.connectStart;
         
         //请求时间
         templeObj.reqTime = item.responseEnd - item.responseStart;
  
         //重定向时间
         templeObj.redirectTime = item.redirectEnd - item.redirectStart;
  
         entryTimesList.push(templeObj);
       }
    });
  ```

  

