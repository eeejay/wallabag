FROM php:8.2-apache
RUN docker-php-ext-configure gd --with-freetype --with-jpeg --with-webp
RUN docker-php-ext-install -j "$(nproc)" \
        bcmath \
        gd \
        gettext \
        iconv \
        intl \
        mbstring \
        opcache \
        pdo \
        pdo_mysql \
        pdo_pgsql \
        pdo_sqlite \
        sockets \
        tidy \
        zip
RUN apt update \
    && apt install -y git curl \
    && curl -sL https://deb.nodesource.com/setup_14.x | bash \
    && apt update \
    && apt-get -y install nodejs \
    && npm i -g jshint;
