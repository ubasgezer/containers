#syntax=docker/dockerfile:1
FROM dunglas/frankenphp:php8.5-alpine
COPY --from=mlocati/php-extension-installer /usr/bin/install-php-extensions /usr/local/bin/

RUN set -eux; \
    apk add --no-cache \
        acl \
        file \
        gettext \
        supervisor \
        nano && \
        (for i in 1 2 3; do install-php-extensions apcu bcmath calendar intl opcache pcntl pdo_mysql protobuf redis soap xsl zip @composer && exit 0; sleep 30; done; exit 1)

ENV APP_ENV=prod
ENV SERVER_ROOT=/var/www/app/public

RUN mv "$PHP_INI_DIR/php.ini-production" "$PHP_INI_DIR/php.ini"

WORKDIR /var/www/app
