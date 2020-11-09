# 使用PHP:7.4-fpm作为基础镜像
FROM php:7.4-fpm

# 作者信息
MAINTAINER TH<1260597728@qq.com>

# 设置环境变量
ENV PHP_CONFIG=/usr/local/bin/php-config PHPIZE=/usr/local/bin/phpize REDIS_EXT=redis-5.3.2

# 安装必要命令工具
RUN apt-get update \
    && apt-get install -y vim \
       openssl \
       libssh-dev


# install composer
RUN curl -sS https://getcomposer.org/installer | php && \
    mv composer.phar /usr/local/bin/composer && \
    composer self-update --clean-backups


# install redis
RUN cd /usr/local/ && \
    curl -o ${REDIS_EXT}.tgz http://pecl.php.net/get/${REDIS_EXT}.tgz && \
    tar zvxf ${REDIS_EXT}.tgz && \
    cd ${REDIS_EXT} && \
    ${PHPIZE} && \
    ./configure --with-php-config=${PHP_CONFIG} && \
    make && make install && \
    cd /usr/local/etc/php/conf.d && \
    echo "extension=redis.so" > ./docker-php-ext-redis.ini

# install swoole
RUN cd /usr/local/ && \
    rm -rf ./swoole-src && \
    curl -o swoole.tar.gz https://github.com/swoole/swoole-src/archive/master.tar.gz -L && \
    tar zxvf swoole.tar.gz && \
    mv swoole-src* swoole-src && \
    cd swoole-src && \
    ${PHPIZE} && \
    ./configure --with-php-config=${PHP_CONFIG} --enable-openssl --enable-http2 && \
    make &&  make install && \
    cd /usr/local/etc/php/conf.d && \
    echo "extension=swoole.so" > ./docker-php-ext-swoole.ini
~                                                                
