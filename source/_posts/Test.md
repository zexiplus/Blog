---
title: web项目测试总结
---

# test

此文档总结了常用测试案例, 例如单元测试,集成测试,端到端测试, 涵盖了常用的测试库



## Table of contents

[TOC]





## unit test



### Jest

Delightful JavaScript Testing https://github.com/facebook/jest



#### quick start

* **download**

  ```shell
  npm i -S jest
  ```

* **config**

  ```json
  {
      "scripts": {
          "test": "jest"
      }
  }
  ```

*  **demo**

  ```js
  // sub.js
  module.exports = function (a) {
      return function (b) {
          return a - b
      }
  }
  
  // sub.test.js
  const sub = require('./sub')
  test('test title: 3 - 2 = 1', () => {
      expect(sub(3)(2)).toBe(1)
  })
  ```

* **run**

  ```shell
  npm run test
  ```



#### Api

> https://jestjs.io/docs/en

* **test**

  定义描述测试

  ```js
  test('your test title', () => {
      // if any test turns failed , test failed
  })
  ```

* **expect**

  期望值

  ```js
  expect(1 + 1).toBe(2)
  ```

* **toBe**

  判断值相等

* **toEqual**

判断对象键值一致

```js
const obj = {a: 1, b: 2}
expect(obj).toEqual()
```

* **toBeNull**

  判断是否为null

* **Number category**

  * toBeGreaterThan
  * toBeLessThan
  * toBeLessThanOrEqual

* **String category**

  * toMatch

    匹配正则

    ```js
    expect('str').not.toMatch(/I/) 
    ```

* **Array category**

  * **toContain**

    包含

    ```js
    expect([1, 2, 3]).toContain(1)
    ```

* **Error category**

  * **toThrow**

    ```js
    function throwErr() { throw new Error('you have an error')}
    expect(throwErr()).toThrow('you have an error')
    ```

* **async test**

  ```js
  function fetchData() {
      return axios.get('demo.json')
  }
  
  test('async test', async () => {
      const data = await fetchData()
      expect(data.id).toBe(12)
  })
  ```



* **hooks**

  jest可以在测试开始前和测试执行之后完成用户指定操作

  * **beforeEach**

    在测试执行前执行操作

    ```js
    beforeEach(() => {
       // do some thing before
    })
    ```

  * **afterEach**

    在测试执行后操作

    ```js
    afterEach(() => {
        // do soem thing after
    })
    ```








## e2e test

###nightWatch



#### 配置文件 nightwatch.conf.js（nightwatch.json）示例

[配置详情](http://nightwatchjs.org/gettingstarted#settings-file)

```js
require('babel-register')
var config = require('../../config')

// http://nightwatchjs.org/gettingstarted#settings-file
module.exports = {
  src_folders: ['test/e2e/specs'], // 测试的文件夹（相对于根目录）
  output_folder: 'test/e2e/reports', // 输出log的文件夹（相对于根目录）
  custom_assertions_path: ['test/e2e/custom-assertions'], //自定义断言文件夹（相对于根目录）

  selenium: {
    //自定义selenium-server 配置
    start_process: true, 
    // selenium-server(测试服务)程序路径 e.g: bin/selenium-server-standalone-2.43.0.jar
    server_path: require('selenium-server').path, 
    host: '127.0.0.1',
    port: 4444,
    cli_args: {
      'webdriver.chrome.driver': require('chromedriver').path
      // 'webdriver.ie.driver', 'webdriver.firefox.profile'
    }
  },

  test_settings: { // 设置全局参数，默认变量
    default: {
      launch_url : "http://localhost", // 可在测试文件browser.lanuchUrl 拿到
      selenium_port: 4444,
      selenium_host: 'localhost',
      silent: true,
      globals: { //全局变量  browser.globals.devServerURL
        devServerURL: 'http://localhost:' + (process.env.PORT || config.dev.port)
      }
    },

    chrome: { // 针对chrome的配置
      desiredCapabilities: {
        browserName: 'chrome',
        javascriptEnabled: true,
        acceptSslCerts: true
      }
    },

    firefox: { // 针对firefox的配置
      desiredCapabilities: {
        browserName: 'firefox', 
        javascriptEnabled: true,
        acceptSslCerts: true
      }
    }
  }
}

```



#### 测试文件 test.js 示例

```js
module.exports = {
  'default e2e tests': function (browser) {
    // automatically uses dev Server port from /config.index.js
    // default: http://localhost:8080
    // see nightwatch.conf.js
    const devServer = browser.globals.devServerURL

    browser
      .url(devServer)
      .waitForElementVisible('#app', 5000)
      .assert.elementPresent('.hello')
      .assert.containsText('h1', 'Welcome to Your Vue.js App')
      .assert.elementCount('img', 1)
      .end()
  }
}

```

####API

[api参考](http://nightwatchjs.org/api)



**Usual**

```js
// 元素选择器 element()
element(selector) // browser.element('#main') 

// 判断 expect
browser.expect.element('#password').to.be.an('input')

// 等待元素可见 
browser.waitForElementVisible('body', 5000)

// 设置input的值
browser.setValue('#username', value)
```



**Expect**

```js
// 链式调用助动词 （没有实际意义）
to,be,been,is,that,which,and,has,have,with,at,does,of

```



**Assert**

```js
.assert  // 测试失败结束测试
.verify // 测试失败跳过，进行下一条测试
```

