FROM php:8.3-rc-apache

RUN apt-get update
RUN apt-get install --yes --force-yes cron g++ gettext libicu-dev openssl libc-client-dev libkrb5-dev libxml2-dev libfreetype6-dev libgd-dev libmcrypt-dev bzip2 libbz2-dev libtidy-dev libcurl4-openssl-dev libz-dev libmemcached-dev libxslt-dev

RUN a2enmod rewrite

RUN apt-get install -y libyaml-dev
RUN pecl install yaml
RUN docker-php-ext-enable yaml

RUN docker-php-ext-configure gd --with-freetype=/usr --with-jpeg=/usr
RUN docker-php-ext-install gd

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/bin --filename=composer

RUN apt-get -y update
RUN apt-get -y install git
RUN apt-get -y install zip

RUN docker-php-ext-install \
    pdo_mysql \
    gettext

COPY ./ /var/www/html/