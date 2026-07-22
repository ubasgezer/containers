#syntax=docker/dockerfile:1
FROM dunglas/frankenphp:php8.5
COPY --from=mlocati/php-extension-installer /usr/bin/install-php-extensions /usr/local/bin/

RUN set -eux; \
    apt-get update && \
    apt-get install -y --no-install-recommends \
        acl \
        file \
        gettext \
        supervisor \
        nano \
        vim && \
        install-php-extensions apcu bcmath calendar intl opcache opentelemetry pcntl pdo_mysql redis soap xsl zip @composer && \
        rm -rf /var/lib/apt/lists/*

ENV APP_ENV=prod
ENV SERVER_ROOT=/var/www/app/public

RUN mv "$PHP_INI_DIR/php.ini-production" "$PHP_INI_DIR/php.ini"

WORKDIR /var/www/app
