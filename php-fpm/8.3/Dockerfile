#syntax=docker/dockerfile:1.4
FROM php:8.3-fpm AS BASE
COPY --from=mlocati/php-extension-installer /usr/bin/install-php-extensions /usr/local/bin/

RUN apt-get update && apt-get install -y acl file gettext git vim nano supervisor libfcgi; git config --global --add safe.directory /var/www;
RUN set -eux; install-php-extensions apcu opcache intl pcntl pdo_mysql redis zip bcmath xsl soap calendar newrelic @composer;

ENV APP_ENV=prod

RUN mv "$PHP_INI_DIR/php.ini-production" "$PHP_INI_DIR/php.ini"

WORKDIR /opt/
