FROM php:7.4-fpm

MAINTAINER TH<1260597728@qq.com>

RUN apt-get update \ 
    && apt-get install -y vim \ 
       openssl \ 
       libssh-dev 

# install composer
RUN curl -sS https://getcomposer.org/installer | php && \
    mv composer.phar /usr/local/bin/composer && \
    composer self-update --clean-backups


# install swoole
ADD swoole.tar.gz /usr/local/src/swoole

RUN cd /usr/local/src/swoole \ 
    && mv swoole-src* swoole-src \ 
    && cd swoole-src \ 
    && /usr/local/bin/phpize \ 
    && ./configure --with-php-config=/usr/local/bin/php-config --enable-openssl \ 
    && make \ 
    && make install \ 
    && cd /usr/local/etc/php/conf.d \ 
    && echo "extension=swoole.so" > ./docker-php-ext-swoole.ini


# install redis
ADD redis-5.3.2.tgz /usr/local/src/redis

RUN cd /usr/local/src/redis/redis-5.3.2 \ 
    && /usr/local/bin/phpize \ 
    && ./configure --with-php-config=/usr/local/bin/php-config \ 
    && make \ 
    && make install \ 
    && cd /usr/local/etc/php/conf.d \
    && echo "extension=redis.so" > ./docker-php-ext-redis.ini
