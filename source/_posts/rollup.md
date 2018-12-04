---
title: rollup 构建工具总结
---



# Rollup

rollup知识点记录



### Table of Content

[TOC]

### Command

##### 命令

* **使用命令行参数打包**, `-o` 指定输出文件名,`-f` 输出文件格式

  ```shell
  rollup src/main.js -o bundle.js -f cjs
  ```

* **命令行使用配置文件打包**

  ```shell
  # 默认使用 rollup.config.js 作为配置文件
  rollup -c
  
  # 指定配置文件
  rollup --config rollup.config.dev.js
  ```


##### 参数 

* 文件格式 `-f`
  * `amd` – AMD规范模块，suitable for RequireJS
  * `cjs` – CommonJS, suitable for Node and Browserify/Webpack
  * `esm` – ES6/7 module file
  * `iife` –  浏览器使用文件 suitable for `<script>` 
  * `umd` –  通用模块 works as `amd`, `cjs` and `iife` 都可以使用
  * `system` – Native format of the SystemJS loader



##### config files

* 单文件打包配置

  ```js
  module.exports = {
    input: 'src/main.js',
    output: {
      file: 'bundle.js',
      format: 'cjs'
    }
  };
  ```

* 多文件打包配置

  ```js
  export default [{
    input: 'main-a.js',
    output: {
      file: 'dist/bundle-a.js',
      format: 'cjs'
    }
  }, {
    input: 'main-b.js',
    output: [
      {
        file: 'dist/bundle-b1.js',
        format: 'cjs'
      },
      {
        file: 'dist/bundle-b2.js',
        format: 'esm'
      }
    ]
  }];
  ```

* 使用插件

  ```js
  import json from 'rollup-plugin-json'
  export default {
      input: 'main.js',
      output: {
          file: 'dist/bundle.js',
          format: 'cjs'
      },
      plugins: [json()]
  }
  ```




### API

* **rollup**

  生成bundle

  ```js
  const inputOptions = {
      input: 'src/main.js',
      plugins: []
  }
  const bundle = await rollup.rollup(inputOptions)
  ```

* **generate**

  生成结果对象

  ```js
  const outputOptions = {
      file: 'dist/output.js',
      format: 'umd'
  }
  const { code, map } = await bundle.generate(outputOptions)
  ```

* **write**

  把生成结果写入硬盘

  ```js
  await bundle.write(outputOptions)
  ```

* **watch**

  检测文件变化并打包

  ```js
  const watchOptions = {}
  const watcher = 
  ```




### Plugins

#### Rollup plugins

##### rollup-plugin-babel

转译ES6/7代码至 ES5

```js
const babel = require('rollup-plugin-babel')
const options = {
    entry: 'main.js',
    ...
    plugins: [babel({
        exclude: 'node_modules/**'
    })]
}
```

> .babelrc   最终确定转译ES6至ES5需要再src文件夹下有一个.babelrc配置文件

```json
{
  "presets": [
    ["env", {
      "modules": false
    }]
  ],
  "plugins": ["external-helpers"]
}
```





##### rollup-plugin-node-resolve, rollup-plugin-commonjs

处理nodepackages中的 Commonjs模块

```js
import resolve from 'rollup-plugin-node-resolve';
import commonjs from 'rollup-plugin-commonjs';
const options = {
    plugins: [
        resolve(),
        commonjs()
    ]
}
```



#### Other plugins

##### bannerjs

* **banner.onebanner() 单行信息注释**
* **banner.multibanner() 多行信息注释**

在生成的文件中插入作者信息， 版本版权等注释信息

```js
const banner = require('bannerjs')
const bundle = await rollup.rollup(options)
const umd = bundle.generate({
    format: 'umd',
    name: 'output',
    banner: banner.multibanner()
})
```



