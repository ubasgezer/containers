#syntax=docker/dockerfile:1.4
# see list on https://hub.docker.com/r/dunglas/frankenphp/tags
ARG PHP_VERSION=latest-php8.3-alpine
FROM dunglas/frankenphp:${PHP_VERSION} AS base

WORKDIR /var/www/app

# persistent / runtime deps
RUN apk add --no-cache acl file gettext git nano supervisor; git config --global --add safe.directory /var/www;
RUN set -eux; install-php-extensions apcu opcache decimal intl pcntl pdo_mysql redis zip bcmath xsl soap @composer;

COPY conf.d/app.ini $PHP_INI_DIR/conf.d/
COPY --chmod=755 docker-entrypoint.sh /usr/local/bin/docker-entrypoint
COPY Caddyfile /etc/caddy/Caddyfile

ENTRYPOINT ["docker-entrypoint"]

HEALTHCHECK --start-period=60s CMD curl -f http://localhost:2019/metrics || exit 1
CMD [ "frankenphp", "run", "--config", "/etc/caddy/Caddyfile" ]

# Dev FrankenPHP image
FROM base AS dev

RUN mv "$PHP_INI_DIR/php.ini-development" "$PHP_INI_DIR/php.ini"
RUN set -eux; install-php-extensions xdebug;
COPY conf.d/app.dev.ini $PHP_INI_DIR/conf.d/

CMD [ "frankenphp", "run", "--config", "/etc/caddy/Caddyfile", "--watch" ]
