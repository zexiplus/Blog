---
title: web前端工程化工具 webpack 重点突破
---

# webpack 学习总结

### 目录

[TOC]



### 开始

* **Download**

  ```shell
  npm i -g webpack@3.6.0
  ```


* **读取参数使用webpack**

  ```shell
  webpack ./entry.js ./output.js
  ```



* **读取配置文件使用 webpack**

  package.json

  ```json
  {
      "dev": "webpack --config ./webpack.dev.config.js",
      "build": "webpack --config ./webpack.prod.config.js"
  }
  ```



### 配置文件结构

  webpack.config.js

  ```js
const path = require('path')
const WebpackHtmlPlugin = require('webpack-html-plugin')
module.exports = {
    // 入口文件 可多个, main 名可自定义
    entry: {
        'main': './main.js'
    },
    // 产出文件
    output: {
        // 指定产出文件目录
        path: path.resolve('./dist')
        filename: './build.js'
    },
    // 监视文件 入口文件变化时自动构建
    watch: true,
    module: {
        loaders: [
            {test: /\.css$/, loader: 'style-loader!css-loader'}
        ]
    },
    plugins: [
        new HtmlWebpackPlugin({
            template: './src/index.html' // 参照物, 把生成的js文件插入此文件
        }),
    ]
    
  }
  ```



* **entry** 

  @Object 入口文件 

* **output** 

  @Object 出口文件 

* **watch** 

  @布尔 是否自动化构建 

* **module** 

  @对象 模块 

* **plugins**

  @数组 插件, 插件的执行顺序与索引有关





### loader 加载器

在js文件中加载css, img等文件**!感叹号用于分割 loader, ? 问号用于传参**



* **样式表加载器 style-loader, css-loader, less-loader**

  main.js

  ```js
  import './main.css'
  ```

  webpack.config.js

  ```js
  modeule.exports = {
      module: {
          loaders: [
              {test: /\.css$/, loader: 'style-loader!css-loader'}
          ]
      }
  }
  ```




* **图片加载器 url-loader**

  **limit 限制图片大小, 单位b**

  main.js

  ```js
  import img from './pic.jpg'
  ```

  ```js
  
  modeule.exports = {
      module: {
          loaders: [
              {	// 图片超过1kb会被生成 一个 1kb的图片, 如果小于1kb, 会被生成base64编码的文件
                  test: /\.(jpg|png|gif|svg)$/, loader: 'url-loader?limit=1000'
              }
          ]
      }
  }
  ```



* **ES67转译加载器 babel-loader**

  ```js
  modeule.exports = {
      module: {
          loaders: [
              {	// 图片超过1kb会被生成 一个 1kb的图片, 如果小于1kb, 会被生成base64编码的文件
                  test: /\.js$/, loader: 'babel-loader', options: {
                      exclude: /node_modules/, // 排除node_modules文件夹
                      presets: ['env'], // 处理es6关键字
                      plugins: ['transform-runtime'] // 处理函数
                  }
              }
          ]
      }
  }
  ```



* **vue-loader**

  ```js
  module.exports = {
      module: {
          loaders: [
              {test: /\.vue$/, loader: 'vue-loader'}
          ]
      }
  }
  ```




### plugins 插件

* webpack-dev-server 

  ```shell
  webpack-dev-server --open --hot --config ./webpack.dev.config.js
  ```

  * --open 自动打开浏览器
  * --hot 热替换, 不刷新的情况下替换
  * --inline 自动刷行
  * --port 9999 定制端口
  * -- process 显示编译进度

* html-webpack-plugin 自动注入插件

* 