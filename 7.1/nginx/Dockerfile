FROM php:7.1-fpm

LABEL maintainer "https://github.com/hurtom/"

RUN curl -L https://getcomposer.org/installer -o composer-setup.php \
    && php composer-setup.php --install-dir=/usr/local/bin --filename=composer \
    && rm -f composer-setup.php

RUN apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 573BFD6B3D8FBC641079A6ABABF5BD827BD9BF62 \
    && echo "deb http://nginx.org/packages/mainline/debian/ jessie nginx" >> /etc/apt/sources.list \
    && apt-get update \
    && apt-get install --no-install-recommends --no-install-suggests -y \
                       libxml2-dev \
                       zlib1g-dev \
                       unzip \
                       git \
                       ca-certificates \
                       supervisor \
                       nginx \
                       nginx-module-xslt \
                       nginx-module-geoip \
                       nginx-module-image-filter \
                       nginx-module-perl \
                       nginx-module-njs \
                       gettext-base \
    && pecl install redis xdebug \
    && docker-php-ext-enable redis xdebug \
    && docker-php-ext-install opcache mysqli pdo_mysql zip \
    && apt-get clean -y \                               
    && rm -rf /var/lib/apt/lists/*

RUN ln -sf /dev/stdout /var/log/nginx/access.log \
    && ln -sf /dev/stderr /var/log/nginx/error.log

COPY supervisord.conf /etc/supervisor/conf.d/supervisord.conf
COPY nginx.conf /etc/nginx/nginx.conf

EXPOSE 80 443

CMD ["supervisord"]
