FROM php:7.4-apache

ARG PSR_VERSION=1.1.0
ARG PHALCON_VERSION=4.1.2
ARG PHALCON_EXT_PATH=php7/64bits

RUN docker-php-ext-install pdo
RUN docker-php-ext-install pdo_mysql

RUN a2enmod rewrite
RUN service apache2 restart

RUN set -xe && \
        # Download PSR, see https://github.com/jbboehr/php-psr
        curl -LO https://github.com/jbboehr/php-psr/archive/v${PSR_VERSION}.tar.gz && \
        tar xzf ${PWD}/v${PSR_VERSION}.tar.gz && \
        # Download Phalcon
        curl -LO https://github.com/phalcon/cphalcon/archive/v${PHALCON_VERSION}.tar.gz && \
        tar xzf ${PWD}/v${PHALCON_VERSION}.tar.gz && \
        docker-php-ext-install -j $(getconf _NPROCESSORS_ONLN) \
            ${PWD}/php-psr-${PSR_VERSION} \
            ${PWD}/cphalcon-${PHALCON_VERSION}/build/${PHALCON_EXT_PATH} \
        && \
        # Remove all temp files
        rm -r \
            ${PWD}/v${PSR_VERSION}.tar.gz \
            ${PWD}/php-psr-${PSR_VERSION} \
            ${PWD}/v${PHALCON_VERSION}.tar.gz \
            ${PWD}/cphalcon-${PHALCON_VERSION} \
        && \
        php -m

COPY docker-phalcon-* /usr/local/bin/

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/bin --filename=composer

RUN apt-get -y update
RUN apt-get -y install git