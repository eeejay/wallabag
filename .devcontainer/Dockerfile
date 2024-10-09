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

ENTRYPOINT ["/entrypoint.sh"]
