# 介绍

Dockerfile文件编译出一个[Nginx](http://www.nginx.org/) 容器镜像。


# 问题

如何安装Docker

```bash
curl -Lk https://get.docker.com/ | sh
```

RHEL、CentOS、Fedora的用户可以使用`setenforce 0`来禁用selinux以达到解决一些问题

当你在issue 提交问题的时候请注意提供一下信息:

- 宿主机的发行版和版本号.
- 使用 `docker version` 命令来给出Docker版本信息.
- 使用 `docker info` 命令来给出进一步信息.
- 提供 `docker run` 命令的详情 (注意打码你的隐私信息).

# 安装

直接使用我们在 [Dockerhub](https://hub.docker.com/r/benyoo/nginx) 上通过自动构建生成的镜像是最为推荐的方式

> **Note**: 也可以在 [Quay.io](https://quay.io/repository/benyoo/nginx)上构建

```bash
docker pull benyoo/nginx:latest
```


#运行
1、常规运行方法：

```bash
docker run -d -p 80:80 -p 443:443 mike666666/nginx:latest
```

​      使用模板配置文件

```bash
mkdir -p /usr/local/nginx && curl -Lk https://github.com/Mike1319/docker-nginx/raw/master/conf.tar| tar xz -C /usr/local/nginx
docker run -d -v /usr/local/nginx/conf:/usr/local/nginx/conf -p 80:80 -p 443:443 benyoo/nginx:latest
```



2、挂载数据目录方法：

```bash
docker run -d -p 80:80 -p 443:443 \
-v /etc/localtime:/etc/localtime:ro \ #将宿主机的时区文件挂载到容器内
-v /data/wwwroot:/data/wwwroot:rw \   #将宿主机的web文件挂载到容器内
-v /data/logs/wwwlogs:/data/wwwlogs:rw \  #将容器内的日志文件挂载到宿主机上
-v /data/conf/nginx/vhost:/usr/local/nginx/conf/vhost:rw \ #将配置文件挂载进容器
mike666666/nginx:latest
```
