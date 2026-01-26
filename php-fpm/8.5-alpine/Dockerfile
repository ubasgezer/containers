#syntax=docker/dockerfile:1
FROM php:8.5-fpm-alpine AS base
COPY --from=mlocati/php-extension-installer /usr/bin/install-php-extensions /usr/local/bin/

RUN set -eux; \
    apk add --no-cache \
        acl \
        file \
        gettext \
        fcgi \
        supervisor \
        nano \
        vim && \
        install-php-extensions apcu opcache intl pcntl pdo_mysql redis zip bcmath xsl soap calendar opentelemetry @composer

ENV APP_ENV=prod

RUN mv "$PHP_INI_DIR/php.ini-production" "$PHP_INI_DIR/php.ini"

WORKDIR /var/www/app

FROM base AS dev

RUN set -eux; \
    apk add --no-cache git; \
    git config --global --add safe.directory /var/www
