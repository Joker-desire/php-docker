FROM php:8.3.9RC1-fpm-alpine3.20
LABEL maintainer="tning6666@gmail.com" version="1.0" license="MIT" description="Swoole5.1.x openssl Xdebug development environment."

COPY docker-php-ext-xdebug.ini /temp/xdebug.ini

RUN php -r "readfile('https://getcomposer.org/installer');" | php \
    && mv /var/www/html/composer.phar /usr/bin/composer

RUN apk update && \
    apk add --no-cache openldap-dev gmp-dev gmp libxml2 && \
    apk add --no-cache libzip-dev libpng libpng-dev libxml2-dev libwebp && \
    apk add --no-cache libwebp-dev libjpeg-turbo libjpeg-turbo-dev freetype && \
    apk add --no-cache freetype-dev libxpm libxpm-dev && \
    apk add --no-cache git ca-certificates autoconf automake libtool && \
    apk add --no-cache cmake file re2c bash && \
    apk add --no-cache pkgconf nginx boost-dev && \
    apk add --no-cache openssh curl curl-dev && \
    apk add --no-cache openssl openssl-dev linux-headers && \
    #  ----------- 安装扩展 -----------
    docker-php-ext-install -j$(nproc) mysqli && \
    docker-php-ext-install -j$(nproc) pdo_mysql && \
    docker-php-ext-install -j$(nproc) gmp && \
    docker-php-ext-install -j$(nproc) zip && \
    docker-php-ext-install -j$(nproc) gd && \
    docker-php-ext-install -j$(nproc) bcmath && \
    docker-php-ext-install -j$(nproc) soap && \
    docker-php-ext-install -j$(nproc) sockets && \
    docker-php-ext-install -j$(nproc) opcache && \
    docker-php-ext-install -j$(nproc) pcntl && \
    docker-php-ext-install -j$(nproc) exif && \
    docker-php-ext-install -j$(nproc) ldap && \
    docker-php-ext-configure gd --with-freetype --with-jpeg --with-webp --with-xpm && \
    docker-php-ext-configure hash --with-mhash && \
    # ----------- 手动编译安装 swoole 开启 openssl 支持 -----------
    cd /tmp && \
    # 下载 Swoole 源码
    git clone https://github.com/swoole/swoole-src.git && \
    cd swoole-src && \
    git checkout 5.1.x && \
    # 配置编译选项
    phpize && \
    ./configure --enable-openssl && \
    # 编译和安装
    make && \
    make install && \
    docker-php-ext-enable swoole && \
    #  ----------- pecl 安装扩展 -----------
    pecl install xdebug redis protobuf && \
    docker-php-ext-enable xdebug redis protobuf && \
    #  ----------- 拷贝 xdebug 配置文件 -----------
    cp /temp/xdebug.ini  /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini && \
    #  ----------- 清理缓存 -----------
    /bin/rm -rf /var/cache/apk/* /tmp/*

WORKDIR /opt/www