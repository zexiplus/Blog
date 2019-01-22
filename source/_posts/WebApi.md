# WEB API

新兴 web api 收集





#### Navigator.sendBeacon()

> 状态： 实验性     [参考](https://developer.mozilla.org/zh-CN/docs/Web/API/Navigator/sendBeacon)

作用： `navigator.sendBeacon()` 方法可用于通过http将少量数据异步传输到Web服务器

```js
window.addEventListener('unload', logData, false);

function logData() {
    navigator.sendBeacon("/log", analyticsData);
}
```

