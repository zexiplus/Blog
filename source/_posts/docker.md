---
Docker learning
---



# Docker learning

docker学习与记录



[TOC]

## Command



| commands                                                 | description                                                  |
| -------------------------------------------------------- | ------------------------------------------------------------ |
| docker images                                            | 列出所有可用镜像                                             |
| docker search httpd                                      | 搜索远程名叫httpd的镜像                                      |
| docker pull httpd                                        | 下载httpd镜像                                                |
| docker run ubuntu echo hello world                       | 在ubuntu系统上运行 echo hello world                          |
| docker run -p 8080:80 -d nginx                           | 运行nginx 并把80端口映射到本机80端口, 会返回一串container的id |
| docker ps                                                | 列出正在运行的container                                      |
| docker cp index.html fae9fa0e6da9://usr/share/nginx/html | 把文件复制到容器目录下(暂时)                                 |
| docker stop fae9fa0e6da9                                 | 停止容器id为fae9fa0e6da9的容器                               |
| docker commit -m 'fun' 66c70c648ea nginx-fun             | 提交对容器的修改并保存                                       |
| docker rmi 66c70c648ea                                   | 删除指定id的镜像                                             |
| docker rm 66c70c648ea                                    | 删除指定id的容器                                             |
| docker build -t container_name .                         | 用dockerfile自定义生成container                              |

