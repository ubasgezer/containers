#syntax=docker/dockerfile:1.4
FROM php:8.3-fpm-alpine AS BASE
COPY --from=mlocati/php-extension-installer /usr/bin/install-php-extensions /usr/local/bin/

RUN apk add --no-cache acl file gettext git nano supervisor fcgi; git config --global --add safe.directory /var/www;
RUN set -eux; install-php-extensions apcu opcache intl pcntl pdo_mysql redis zip bcmath xsl soap @composer;

ENV APP_ENV=prod

RUN mv "$PHP_INI_DIR/php.ini-production" "$PHP_INI_DIR/php.ini"

WORKDIR /opt/newrelic/

RUN wget https://download.newrelic.com/php_agent/release/newrelic-php5-10.17.0.7-linux-musl.tar.gz; \
    tar -xvzf newrelic-php5-10.17.0.7-linux-musl.tar.gz; \
    cd newrelic-php5-10.17.0.7-linux-musl; \
    NR_INSTALL_SILENT=true ./newrelic-install install;
