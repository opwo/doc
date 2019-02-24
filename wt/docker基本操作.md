# docker命令

## 启动docker

```sh
#centos7为例
systemctl start docker
#关闭docker
systemctl stop docker
#系统下次开机自动启动
systemctl enable docker
```

## 搜索镜像

```sh
docker search xxxx
#也可以访问 https://hub.docker.com(推荐)
```

## 拉取（下载安装）镜像

```shell
docker pull xxxx #默认最新版本，也可以是 docker pull xxx:latest

#指定某个版本(镜像后加 “:” 和版本号)
docker pull xxx:5.5
```

## 查看已有的镜像

```sh
docker images
```

## 运行镜像

```sh
docker run --name myImgname -d image # --name: 给镜像指定一个别名myImgname(可不指定); -d:代表后台运行，image代表要运行的镜像名,如果是对个版本的镜像，需要指定镜像版本image:x.x 否则默认最新版本

#举例：启动一个做了端口映射的Tomcat。
docker -run -d -p 8888:8080 tomcat #-d:后台运行，-P:端口映射（主机端口:容器端口）

```

## 查看运行中的容器

```sh
docker ps
```

## 停止运行的容器

```sh
docker stop name/id # 可以是容器的名字或者ID
```

## 查看所有的容器

```sh
docker ps -a
```

## 启动容器

```sh
docker start 容器ID
```

## 删除容器

```sh
#先停止容器再删除
docker rm 容器ID
```

## 查看容器日志

```sh
docker logs container-name/container-id
```

# 实例

## install mysql image

```sh
#先下载镜像 
docker pull mysql
#运行
docker run -p 3306:3306 --name mysql01 -e MYSQL_ROOT_PASSWORD=123456 -d mysql
```

## 号外

```sh
#linux防火墙相关
service firewalld status #查看防火墙状态
service firewalld stop #关闭防火墙
```

