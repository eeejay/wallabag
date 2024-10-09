FROM mcr.microsoft.com/devcontainers/php:1-8.2-bullseye
RUN apt-get -y update && \
    apt-get install -y libicu-dev libtidy-dev libpng-dev libjpeg-dev libwebp-dev libfreetype6-dev
RUN docker-php-ext-configure gd --with-freetype --with-jpeg --with-webp
RUN docker-php-ext-install gd tidy intl sockets

RUN mv "${PHP_INI_DIR}/php.ini-development" "${PHP_INI_DIR}/php.ini"

RUN curl -L -o /usr/local/bin/envsubst https://github.com/a8m/envsubst/releases/download/v1.1.0/envsubst-`uname -s`-`uname -m`; \
    chmod +x /usr/local/bin/envsubst

COPY "../docker/php/entrypoint.sh" "/entrypoint.sh"
COPY "../docker/php/config/" "/opt/wallabag/config/"

RUN mkdir -p \
        /var/www/html/app/config/ \
        /var/www/html/var/cache \
        /var/www/html/web/assets \
        /var/www/html/data \
        /var/www/html/data/db \
        /var/www/.cache

ENTRYPOINT ["/entrypoint.sh"]
CMD ["php", "bin/console", "--env=dev", "server:run", "0.0.0.0:8000"]

FROM rootless AS default

ARG USER_UID=1000
ARG USER_GID=1000

RUN groupmod -g 1000 www-data ; \
    usermod -u ${USER_UID} -g www-data www-data ; \
    touch /usr/local/etc/php/conf.d/wallabag-php.ini \
        /var/www/.yarnrc ; \
    chown -R www-data: /var/www/html \
        /usr/local/etc/php/conf.d/wallabag-php.ini \
        /var/www/.cache \
        /var/www/.yarnrc

USER www-data
