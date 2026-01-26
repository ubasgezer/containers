#syntax=docker/dockerfile:1.4
FROM php:8.3-fpm AS BASE
COPY --from=mlocati/php-extension-installer /usr/bin/install-php-extensions /usr/local/bin/

RUN set -eux; \
    apt-get update && \
    apt-get install -y --no-install-recommends \
        acl \
        file \
        gettext \
        git \
        libfcgi \
        supervisor \
        nano \
        vim && \
        git config --global --add safe.directory /var/www && \
        install-php-extensions apcu opcache intl pcntl pdo_mysql redis zip bcmath xsl soap calendar newrelic @composer && \
        rm -rf /var/lib/apt/lists/*

ENV APP_ENV=prod

RUN mv "$PHP_INI_DIR/php.ini-production" "$PHP_INI_DIR/php.ini"

WORKDIR /opt/
