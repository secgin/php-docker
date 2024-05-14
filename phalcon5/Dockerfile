FROM php:8.2-apache-buster

ARG PHALCON_VERSION=5.6.0

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