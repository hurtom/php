FROM alpine:3.6

LABEL maintainer "https://github.com/hurtom/"

RUN addgroup -g 82 -S www-data \
    && adduser -u 82 -D -S -G www-data www-data

RUN apk add --no-cache \
    ca-certificates \
    curl \
    git \
    nginx \
    nginx-mod-http-image-filter \
    nginx-mod-http-geoip \
    php7 \
    php7-bcmath \
    php7-common \
    php7-ctype \
    php7-curl \
    php7-dom \
    php7-fileinfo \
    php7-fpm \
    php7-gd \
    php7-gettext \
    php7-iconv \
    php7-json \
    php7-mbstring \
    php7-mysqli \
    php7-mysqlnd \
    php7-opcache \
    php7-openssl \
    php7-pdo_mysql \
    php7-pdo_sqlite \
    php7-phar \
    php7-posix \
    php7-redis \
    php7-session \
    php7-simplexml \
    php7-sqlite3 \
    php7-tokenizer \
    php7-xdebug \
    php7-xml \
    php7-xmlreader \
    php7-xmlwriter \
    php7-zip \
    php7-zlib \
    runit \
    tzdata

RUN curl -L https://getcomposer.org/installer -o composer-setup.php \
    && php composer-setup.php --install-dir=/usr/local/bin --filename=composer \
    && rm -f composer-setup.php

RUN cp /usr/share/zoneinfo/Europe/Kiev /etc/localtime \
    && echo "Europe/Kiev" > /etc/timezone

COPY runit /etc/runit
COPY nginx.conf /etc/nginx/nginx.conf
COPY www.conf /etc/php7/php-fpm.d/www.conf

RUN sed -i "/\[global\]/a daemonize = no" /etc/php7/php-fpm.conf \
    && sed -i "/\[global\]/a error_log = /proc/self/fd/2" /etc/php7/php-fpm.conf

RUN find /etc/runit -type f -exec chmod +x {} \;

RUN ln -sf /dev/stdout /var/log/nginx/access.log \
    && ln -sf /dev/stderr /var/log/nginx/error.log

EXPOSE 80 443

WORKDIR /var/www/html

CMD ["runsvdir", "/etc/runit"]
