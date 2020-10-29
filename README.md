# docker-nginx-fpm-swoole-mysql-redis
docker 容器中搭建两套PHP开发模式。一套fpm、一套swoole。两套通过不同的端口去运行

## nginx
nginx 用的是最新的镜像，直接在docker中 docker pull nginx就行

## php
PHP 用的是7.4-fpm的镜像。其中自己在此基础上增加了composer、swoole、redis扩展。

## mysql
mysql 用的是5.7的镜像，直接在docker中 docker pull mysql:5.7就行

## redis
redis 用的是5.0.5的镜像，直接在docker中 docker pull redis:5.0.5就行


## 整体结构目录

|-- docker
    |-- compose
    |   |-- dev
    |   |   |-- nginx-fpm-swoole-mysql-redis
    |   |   |   |-- docker-compose.yaml
    |-- dockerfile
    |   |-- php-swoole-redis
    |   |   |-- Dockerfile
    |   |   |-- redis-5.0.5.tgz
    |   |   |-- swoole.tar.gz
    |   |-- post.md
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
    
