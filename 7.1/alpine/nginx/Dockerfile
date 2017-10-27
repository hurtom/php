FROM php:7.1-fpm-alpine3.4

LABEL maintainer "https://github.com/hurtom/"

RUN curl -L https://getcomposer.org/installer -o composer-setup.php \
    && php composer-setup.php --install-dir=/usr/local/bin --filename=composer \
    && rm -f composer-setup.php

RUN apk add --no-cache --virtual .build-deps \
            $PHPIZE_DEPS \
            freetype-dev \
            gettext-dev \
            libjpeg-turbo-dev \
            libpng-dev \
            zlib-dev \
    && pecl install redis xdebug \
    && docker-php-ext-enable redis xdebug \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install bcmath gd gettext mysqli opcache pdo_mysql zip \
    && apk del .build-deps

RUN apk add --no-cache \
            ca-certificates \
            freetype \
            git \
            libjpeg-turbo \
            libintl \
            libpng \
            tzdata \
            unzip \
    && apk add --no-cache --repository http://dl-cdn.alpinelinux.org/alpine/v3.6/main \
            nginx \
    && apk add --no-cache --repository http://dl-cdn.alpinelinux.org/alpine/v3.6/community \
            runit

RUN cp /usr/share/zoneinfo/Europe/Kiev /etc/localtime \
    && echo "Europe/Kiev" > /etc/timezone

RUN sed -ri 's/^www-data:x:82:82:/www-data:x:1000:1000:/' /etc/passwd

RUN sed -ri '/^access.log/ s/^/; /' /usr/local/etc/php-fpm.d/docker.conf \
    && sed -ri "s/^pm = dynamic/pm = ondemand/" /usr/local/etc/php-fpm.d/www.conf

RUN ln -sf /dev/stdout /var/log/nginx/access.log \
    && ln -sf /dev/stderr /var/log/nginx/error.log

EXPOSE 80

COPY runit /etc/runit

RUN find /etc/runit -type f -exec chmod +x {} \;

CMD ["runsvdir", "/etc/runit"]
