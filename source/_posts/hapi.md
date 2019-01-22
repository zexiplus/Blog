# hapi

hapi 学习记录



## contents

[TOC]

### 参考

[官方中文文档](https://hapijs.com/tutorials/getting-started?lang=zh_CN)

[基于 hapi 的 Node.js 小程序后端开发实践指南](https://juejin.im/book/5b63fdba6fb9a04fde5ae6d0)





### 初始化

**新建项目**

```shell
npm init
```

**下载hapi v16**

```shell
npm i hapi@16
```



### 调试

**自监测启动**

```shell
supervisor app.js
```

**普通 chrome 调试**

```shell
node --inspect app.js
```

**自启动chrome调试**

```shell
supervisor --inspect app.js
```

**vscode 调试**

新建编辑`.vscode/launch.json`, 编辑`program`字段，设置断点， 点击启动程序，请求程序，观察值。 

> .vscode/launch.json

```json
{
  "version": "0.2.0",
  "configurations": [
    {
      "type": "node",
      "request": "launch",
      "name": "启动程序",
      "program": "${workspaceFolder}\\app.js"
    }
  ]
}
```

