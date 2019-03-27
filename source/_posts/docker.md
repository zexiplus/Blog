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
| docker stop fae9fa0e6da9                                 | 停止容器id为fae9fa0e6da9的容器                               |
| docker cp index.html fae9fa0e6da9://usr/share/nginx/html | 把文件复制到容器目录下(暂时)                                 |
|                                                          |                                                              |
| docker commit -m 'fun' 66c70c648ea nginx-fun             | 提交对容器的修改并保存                                       |
| docker rmi 66c70c648ea                                   | 删除指定id的镜像                                             |
| docker rm 66c70c648ea                                    | 删除指定id的容器                                             |
| docker build -t container_name .                         | 用dockerfile自定义生成container                              |



### Dockerfile

**第一个Dockerfile**

`Dockerfile`

```dockerfile
FROM alpine:latest
MAINTAINER float
CMD echo 'hello docker'
```

**第二个Dockerfile**

```dockerfile
FROM ubuntu
MAINTAINER float
RUN apt-get update
RUN apt-get install -y nginx
COPY index.html /var/www/html
ENTRYPOINT ["/usr/sbin/nginx", "-g", "daemon off;"]
EXPOSE 80
```

**运行**

```shell
docker build -t imageName .
```



**Dockerfile语法**

| 命令       | 用途         |
| ---------- | ------------ |
| FROM       | base image   |
| RUN        | 执行命令     |
| ADD        | 添加文件     |
| COPY       | 拷贝文件     |
| CMD        | 执行命令     |
| EXPOSE     | 暴露端口     |
| WORKDIR    | 指定路径     |
| MAINTAINER | 维护者       |
| ENV        | 指定环境变量 |
| ENTRYPOINT | 容器入口     |
| USER       | 指定用户     |
| VOLUME     | Mount point  |



### Registry

| 命令                                                   | 含义     |
| ------------------------------------------------------ | -------- |
| docker search whalesay                                 | 搜索仓库 |
| docker pull docker/whalesay                            | 拉取镜像 |
| docker run docker/whalesay cowsay Docker is really fun |          |



### docker-compose

| 命令                 | 含义     |
| -------------------- | -------- |
| docker-compose up -d | 开启服务 |
| docker-compose stop  | 停掉服务 |
| docker-compose rm    | 删除镜像 |

