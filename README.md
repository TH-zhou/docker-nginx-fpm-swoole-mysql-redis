# docker-nginx-fpm-swoole-mysql-redis
docker 容器中搭建两套PHP开发模式。一套fpm、一套swoole。两套通过不同的端口去运行

## nginx
nginx 用的是最新的镜像，直接在docker中 docker pull nginx就行

## php
PHP 用的是7.4-fpm的镜像。其中自己在此基础上增加了composer、swoole、redis扩展。

## mysql
mysql 用的是5.7的镜像，直接在docker中 docker pull mysql:5.7就行

## redis
redis 用的是最新的镜像，直接在docker中 docker pull redis就行

## 前期工作 重要
把各镜像pull下来之后，docker run -itd --rm 镜像名 得到容器ID之后呢，把对应需要的配置文件及数据cp下来。docker cp 容器ID:/docker容器中的目录和文件 ./宿主机的目录或者文件
一旦挂载之后呢，宿主机没有这些目录会自动创建，文件也是空白的，导致挂载过去会把docker中相应的配置文件也给同步掉，也变成空白文件

## 启动前工作
先进入dockerfile目录下构建自己的PHP镜像。添加composer、redis、swoole等扩展

## 启动
进入到compose/dev/nginx-fpm-swoole-mysql-redis 目录下，直接 docker-compose up


## 整体结构目录
|-- docker

    |-- compose
    |   |-- dev
    |   |   |-- nginx-fpm-swoole-mysql-redis
    |   |   |   |-- docker-compose.yaml
    |-- dockerfile
    |   |-- php-swoole-redis
    |   |   |-- Dockerfile
    |-- mysql
    |   |-- conf
    |   |   |-- conf.d
    |   |   |   |-- docker.cnf
    |   |   |   |-- mysql.cnf
    |   |   |   |-- mysqldump.cnf
    |   |   |-- mysql.conf.d
    |   |   |   |-- mysqld.cnf
    |   |-- data
    |   |   |-- mysql中对应的库、表文件
    |-- nginx
    |   |-- conf.d
    |   |   |-- fpm.conf
    |   |   |-- swoole.conf
    |   |-- logs
    |   |-- nginx.conf
    |-- php
    |   |-- logs
    |   |-- php-fpm.conf
    |   |-- php-fpm.d
    |   |   |-- docker.conf
    |   |   |-- www.conf
    |   |   |-- zz-docker.conf
    |-- redis
    |   |-- conf
    |   |   |-- redis.conf
    |   |-- data
    |-- work
    |   |-- fpm
    |   |   |-- phpinfo.php
    |   |-- html
    |   |   |-- 50x.html
    |   |   |-- index.html
    |   |-- swoole
    |   |   |-- server.php
