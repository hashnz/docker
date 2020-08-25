FROM php:7.4-fpm-alpine

RUN apk update \
    && apk add --no-cache --update --virtual buildDeps $PHPIZE_DEPS \
    # libmpdec is requirement of decimal, seems the only way to install on alpine:
    && apk add autoconf git libpng libpng-dev freetype-dev libjpeg-turbo-dev \
    && git clone --branch master --depth 1 https://github.com/bematech/libmpdec.git \
    && cd libmpdec \
    && ./configure \
    && make \
    && make install \
    && cd .. \
    # /libmpdec
    && apk add icu-dev openssl-dev \
    && docker-php-source extract \
    && pecl install xdebug \
    && pecl install redis \
    && pecl install mongodb \
    && pecl install decimal \
    && docker-php-ext-install pdo_mysql intl \
    && docker-php-ext-install gd \
    && docker-php-ext-install exif \
    && docker-php-ext-enable opcache xdebug redis mongodb decimal gd exif \
    && docker-php-source delete \
    && apk del buildDeps

# composer
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer
ENV COMPOSER_ALLOW_SUPERUSER=1
RUN composer global require hirak/prestissimo

CMD ["php-fpm"]
