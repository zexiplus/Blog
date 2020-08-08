---
title: gulp
---
# gulp

> 参考1 <https://github.com/nimojs/gulp-book>
>
> 参考2 https://www.kancloud.cn/thinkphp/gulp-guide/43998



## table of contents

[TOC]



## start

gulp 是基于 node 实现 Web 前端自动化开发的工具，利用它能够极大的提高开发效率。

在 Web 前端开发工作中有很多“重复工作”，比如压缩CSS/JS文件。而这些工作都是有规律的。**找到这些规律，并编写 gulp 配置代码,让 gulp 自动执行这些“重复工作”**



### 将规律转换为 gulp 代码

现有目录结构如下：

```
└── src/
	└── js/
    	└── a.js
```

#### 规律

1. 找到src/ js目录下的所有 .js 文件
2. 压缩这些 js 文件
3. 将压缩后的代码另存在 dist/js/ 目录下

#### 编写 gulp 代码

```js
// 压缩 JavaScript 文件
gulp.task('script', function() {
    // 1. 找到
    gulp.src('src/js/*.js')
    // 2. 压缩
        .pipe(uglify())
    // 3. 另存
        .pipe(gulp.dest('dist/js'));
});
```

#### 代码执行结果

代码执行后文件结构

```
└── js/
│   └── a.js
└── dist/
    └── js/
        └── a.js
```

a.js 压缩前

```js
function demo (msg) {
    console.log('--------\r\n' + msg + '\r\n--------')
}

demo('Hi')
```

a.js 压缩后

```js
function demo(n){console.log("--------\r\n"+n+"\r\n--------")}demo("Hi");
```

此时 `dist/js` 目录下的 `.js` 文件都是压缩后的版本。



#### 功能

你还可以监控 (watch) `js/` 目录下的 js 文件，当某个文件被修改时，自动压缩修改文件

------

gulp 还可以做很多事，例如：

1. 压缩CSS
2. 压缩图片
3. 编译Sass/LESS
4. 编译CoffeeScript
5. markdown 转换为 html



#### 安装

**全局安装gulp 命令**

```shell
npm i -g gulp-cli
```

**在项目内安装 gulp依赖**

```shell
npm i -D gulp
```





## gulp 压缩 js



### 安装

```shell
npm i -D gulp-uglify
```



新建一个`glupfile.js`, 内容如下

```js
const gulp = require('gulp')
const uglify = require('gulp-uglify')

// 定义任务, 命令行执行 gulp script 运行以下任务
const scriptTask = function () {
  gulp
  .src('src/js/*.js')
  .pipe(uglify())
  .pipe(gulp.dest('dist/js'))
}
gulp.task('script', scriptTask)

// 运行 gulp auto 后， 当 watch 文件变化后， 自动执行 script 任务
gulp.task('auto', function() {
  gulp.watch('src/js/*.js', () => {
    console.log('changed')
    scriptTask()
  })
})


// 定义默认任务 命令行执行 gulp
gulp.task('default', function() {
  gulp.series('script', 'auto')
})
```

```shell
# 执行默认任务
gulp
# 执行 script 任务
gulp script
```



### API

- `gulp.task(name, fn)` - 定义任务，第一个参数是任务名，第二个参数是任务内容。
- `gulp.src(path)` - 选择文件，传入参数是文件路径。
- `gulp.dest(path)` - 输出文件
- `gulp.pipe()` - 管道，你可以暂时将 pipe 理解为将操作加入执行队列
- `gulp.series(taskname)` 串行执行已定义的 gulp task，taskname 可以为字符串或函数





## gulp 压缩 css

### 安装

压缩css需要安装 gulp-minify-css插件

```shell
npm i -D gulp-minify-css
```



增加 css 任务， `gulpfile.js` 如下

```js
const gulp = require('gulp')
const uglify = require('gulp-uglify')
const minifyCSS = require('gulp-minify-css')

const cssTask = function() {
  gulp
    .src('src/css/*.css')
    .pipe(minifyCSS())
    .pipe(gulp.dest('dist/css'))
}
gulp.task('css', cssTask)
```

```shell
# 执行
gulp css
```





## gulp 编译 less

gulp编译less需要下载 `gulp-less`插件



### 安装

```shell
npm i -D gulp-less
```

`gulpfile.js`

```js
const gulp = require('gulp')
const lessCompile require('gulp-less')

// 编译less
const lessTask = function() {
  gulp
    .src('src/less/*.less')
    .pipe(lessCompile())
    .pipe(minifyCSS())
    .pipe(gulp.dest('dist/css'))
}
gulp.task('less', lessTask)
```

```shell
# 执行命令编译less并压缩
gulp less
```





## gulp 压缩 图片

### 安装

压缩图片需要安装 gulp-imagemin

```shell
npm i -D gulp-imagemin
```



`gulpfile.js`

```js
const gulp = require('gulp')
const imageMin = require('gulp-imagemin')

const imgTask = function() {
  gulp
    .src('src/imgs/*.*')
    .pipe(imageMin({
      progressive: true
    }))
    .pipe(gulp.dest('dist/imgs'))
}
gulp.task('imgs', imgTask)
```

```shell
# 执行压缩图片
gulp imgs
```



## gulp 处理css 生成前缀

### 安装

安装依赖 `gulp-autoprefixer`

```shell
npm i -D gulp-autoprefixer
```

### 使用

```js
const gulp = require('gulp')
const sourceMap = require('gulp-autoprefixer')

// 生成css前缀
const cssWithPrefixTask = function() {
  gulp
    .src('src/css/*.css')
    .pipe(sourceMap.init())
    .pipe(autoprefix({
      browsers: 'last 2 versions'
    }))
    .pipe(minifyCSS())
    .pipe(sourceMap.write('./'))
    .pipe(gulp.dest('dist/css'))
}
gulp.task('cssWithPrefix', cssWithPrefixTask)
```

```shell
# 启动任务
gulp cssWithPrefix
```



## gulp 压缩生成 source map

### 安装

安装依赖 `gulp-sourcemaps`

```shell
npm i -D gulp-sourcemaps
```

### 使用

```js
const gulp = require('gulp')
const sourceMap = require('gulp-sourcemaps')

// 压缩代码并生成 sourcemap
const scriptWithMapTask = function() {
  gulp
    .src('src/js/*.js')
    .pipe(sourceMap.init())
    .pipe(uglify())
    .pipe(sourceMap.write('/'))
    .pipe(gulp.dest('dist/js'))
}
gulp.task('scriptWithMap', scriptWithMapTask)
```

```shell
gulp scriptWithMap
```

