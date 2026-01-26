#syntax=docker/dockerfile:1
FROM php:8.5-fpm AS base
COPY --from=mlocati/php-extension-installer /usr/bin/install-php-extensions /usr/local/bin/

RUN set -eux; \
    apt-get update && \
    apt-get install -y --no-install-recommends \
        acl \
        file \
        gettext \
        libfcgi \
        supervisor \
        nano \
        libfcgi-bin \
        vim && \
        install-php-extensions apcu opcache intl pcntl pdo_mysql redis zip bcmath xsl soap calendar opentelemetry @composer && \
        rm -rf /var/lib/apt/lists/*

ENV APP_ENV=prod

RUN mv "$PHP_INI_DIR/php.ini-production" "$PHP_INI_DIR/php.ini"

WORKDIR /var/www/app

FROM base AS dev

RUN set -eux; \
    apt-get update; \
    apt-get install -y --no-install-recommends \
        git; \
    git config --global --add safe.directory /var/www; \
    rm -rf /var/lib/apt/lists/*
