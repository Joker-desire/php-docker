FROM php:8.2-apache

RUN php -r "readfile('https://getcomposer.org/installer');" | php \
    && mv /var/www/html/composer.phar /usr/bin/composer
RUN apt clean \
    && apt-get update \
    && apt-get -y install libzip-dev libicu-dev \
    && docker-php-ext-install mysqli zip intl \
    && pecl install xdebug \
    && docker-php-ext-enable xdebug \
    && echo "xdebug.mode=debug" >> /usr/local/etc/php/php.ini
