FROM php:5.6-fpm

LABEL maintainer "https://github.com/hurtom/"

RUN curl -L https://getcomposer.org/installer -o composer-setup.php \
    && php composer-setup.php --install-dir=/usr/local/bin --filename=composer \
    && rm -f composer-setup.php

RUN apt-get update \
    && apt-get install --no-install-recommends --no-install-suggests -y \
                       libxml2-dev \
                       zlib1g-dev \
                       unzip \
                       git \
                       ca-certificates \
    && pecl install redis xdebug \
    && docker-php-ext-enable redis xdebug \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install bcmath gd mysqli opcache pdo_mysql zip \
    && apt-get clean -y \                    
    && rm -rf /var/lib/apt/lists/*
