FROM php:8.3-apache

ARG PHALCON_VERSION=5.8.0

RUN set -xe && \
        cd / && \
        docker-php-source extract && \
        # Install ext-phalcon
        curl -sSLO https://github.com/phalcon/cphalcon/archive/v${PHALCON_VERSION}.tar.gz && \
        tar xzf /v${PHALCON_VERSION}.tar.gz && \
        docker-php-ext-install -j $(getconf _NPROCESSORS_ONLN) \
            /cphalcon-${PHALCON_VERSION}/build/phalcon \
        && \
        # Remove all temp files
        rm -r \
            /v${PHALCON_VERSION}.tar.gz \
            /cphalcon-${PHALCON_VERSION} \
        && \
        docker-php-source delete && \
        php -m

COPY docker-phalcon-* /usr/local/bin/

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/bin --filename=composer

RUN apt-get -y update
RUN apt-get -y install git
RUN apt-get -y install zip

RUN docker-php-ext-install \
    pdo_mysql

RUN a2enmod rewrite
RUN service apache2 restart