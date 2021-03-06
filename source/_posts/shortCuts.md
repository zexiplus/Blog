---
title: 系统/软件快捷键和配置定义
---

# shortcuts

> 保存了系统/软件快捷键和配置定义,以便查看使用   ←↑→↓



#### windows

| windows系统快捷键说明     | 快捷键                 |
| ------------------------- | ---------------------- |
| 在当前文件夹下打开cmd窗口 | **shift + rightMouse** |



#### mac

| mac 快捷键说明       | 快捷键                             |
| -------------------- | ---------------------------------- |
| 锁屏                 | **ctrl + command + q**             |
| 搜索文件             | **command + 空格**                 |
| 工作区缩略图         | **Ctrl + Tab**                     |
| 打开App菜单          | **option + A**                     |
| 打开launchpad        | **option + D**                     |
| 更改文件默认启动软件 | **鼠标右键 / getinfo / open with** |
| 系统截全屏           | **command + shift + 3**            |
| 截部分屏幕           | **command + shift + 4**            |
| 连接远程文件夹       | **command+ k**                     |
| 预览图片             | **选中图片 + space**               |
|                      |                                    |



#### Shell

**autojump**

| 命令                          | 含义                                     |
| ----------------------------- | ---------------------------------------- |
| j -a D '/Users/float/Desktop' | 添加快捷目录/Users/float/Desktop为别名 D |
| j D                           | 跳转到/Users/float/Desktop 目录          |





#### vsCode

> 插件介绍 https://zhuanlan.zhihu.com/p/27905838

> 修改编辑器快捷键 **code/ 首选项/ 键盘快捷方式**

| vsCode 快捷键说明                 | 按键                                      |
| --------------------------------- | ----------------------------------------- |
| 开启命令面板                      | **command + shift + p**                   |
| 转到定义                          | **command + option + ↓**                  |
| 开启/切换终端面板                 | **ctrl + `**                              |
| 格式化代码                        | **option + shift + f**                    |
| 把文件夹在 finder 中显示          | **command + option + R**                  |
| 向上移动行                        | **option + ↓**                            |
| 预览markdown文件                  | **command + K V**                         |
| 启用调试                          | **F5**                                    |
| 启用多行编辑                      | **option + 鼠标选择**                     |
| 在文件夹中查找                    | **command + shift + F**                   |
| 启用quokka                        | **command + K Q**                         |
| 停用quokka                        | **command + K S**                         |
| 使用markdonw toc 插件生成文档目录 | **markdown 中右键 , markdown toc insert** |
| 使用expand-region 选中括号内内容  | **command + shift + M**                   |
| 注册code 系统命令                 | **command + shift + P >  shell code**     |
| 在命令行中使用vscode              | **code main.js**                          |
| 插入假数据                        | 命令面板 输入 faker                       |

* **js debug 配置说明**

  | 参数                       | 说明                                                     |
  | -------------------------- | -------------------------------------------------------- |
  | ${workspaceRoot}           | VSCode中打开文件夹的路径                                 |
  | ${workspaceRootFolderName} | (VSCode中打开文件夹的路径, 但不包含"/"                   |
  | ${file}                    | (当前打开的文件                                          |
  | ${relativeFile}            | 当前打开的文件,相对于workspaceRoot                       |
  | ${fileBasename}            | 当前打开文件的文件名, 不含扩展名                         |
  | ${fileDirname}             | 当前打开文件的目录名                                     |
  | ${fileExtname}             | 当前打开文件的扩展名                                     |
  | ${cwd}                     | the task runner's current working directory on startup() |

  **配置示例** 

  ```json
  {
      "version": "0.2.0",
      "configurations": [
          {
              "type": "node",
              "request": "launch",
              "name": "Launch Program",
              "program": "${workspaceFolder}/${relativeFile}"
          },
          {
              "type": "chrome",
              "request": "launch",
              "name": "Launch Chrome against localhost",
              "url": "http://localhost:8080",
              "webRoot": "${workspaceFolder}"
          }
      ]
  }
  ```


#### sublime 

| sublime快捷键说明          | 快捷键                          |
| -------------------------- | ------------------------------- |
| 编译执行代码               | **ctrl + B**                    |
| 复制当前行到下一行         | **ctrl + shift + d**            |
| 移动当前行                 | **ctrl + shift + 上下左右箭头** |
| 选中花括号里面的全部内容   | **Ctrl+Shift+M**                |
| 可快速选中一行中的某一部分 | **shift + ctrl然后按←或→**      |

 

#### chrome

| chrome 快捷键说明    | 快捷键                 |
| -------------------- | ---------------------- |
| 重新打开刚关闭的页面 | **Shift + Ctrl + T**   |
| (mac) 打开开发者工具 | option + commond + I   |
| (mac) 清除系统缓存   | command + shift + back |
| (mac) 后退           | command + [            |



