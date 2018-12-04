---
title: nodejs tips总结
---



# Node Tips

node 常用语句记录



### File Operator

* **给定文件路径dest, 判断文件夹是否存在**

  ```js
  const dest = 'dist/index.js'
  fs.existsSync(path.dirname(dest))
  ```

* **给定路径dest， 创建文件夹**

  ```js
  fs.mkdirSync(path.dirname(dest))
  ```

* **返回已A为基准的B的相对路径**

  ```js
  const A = '/data/orandea/test/aaa'
  const B = '/data/orandea/impl/bbb'
  path.relative(A, B) // return '../../impl/bbb'
  ```






