FROM php:7.3-fpm-alpine

RUN apk add --no-cache --update --virtual buildDeps $PHPIZE_DEPS \
    && apk add icu-dev \
    && docker-php-source extract \
    && pecl install xdebug \
    && pecl install redis \
    && docker-php-ext-install pdo_mysql intl \
    && docker-php-ext-enable opcache xdebug redis \
    && docker-php-source delete \
    && apk del buildDeps

# composer
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer
ENV COMPOSER_ALLOW_SUPERUSER=1
RUN composer global require hirak/prestissimo

CMD ["php-fpm"]
