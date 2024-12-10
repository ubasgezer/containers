#syntax=docker/dockerfile:1.4
FROM php:8.4-fpm AS BASE
COPY --from=mlocati/php-extension-installer /usr/bin/install-php-extensions /usr/local/bin/

RUN apt-get update && apt-get install -y acl file gettext git vim nano supervisor libfcgi; git config --global --add safe.directory /var/www;
RUN set -eux; install-php-extensions apcu opcache intl pcntl pdo_mysql redis zip bcmath xsl soap calendar @composer;

ENV APP_ENV=prod

RUN mv "$PHP_INI_DIR/php.ini-production" "$PHP_INI_DIR/php.ini"

WORKDIR /opt/

RUN NEWRELIC_FILE=$(curl -s https://download.newrelic.com/php_agent/release/ | grep -Eo 'newrelic-php5-([0-9]+\.?)+-linux\.tar\.gz' | head -n 1) || exit && \
    curl -s -L https://download.newrelic.com/php_agent/release/${NEWRELIC_FILE} | tar xvz && \
    NR_INSTALL_SILENT=true /opt/${NEWRELIC_FILE%.tar.gz}/newrelic-install install;