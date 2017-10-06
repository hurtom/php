FROM alpine:3.6

LABEL maintainer "https://github.com/hurtom/"

RUN addgroup -g 82 -S www-data \
    && adduser -u 82 -D -S -G www-data www-data

RUN apk add --no-cache \
    ca-certificates \
    curl \
    git \
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
    tzdata

RUN curl -L https://getcomposer.org/installer -o composer-setup.php \
    && php composer-setup.php --install-dir=/usr/local/bin --filename=composer \
    && rm -f composer-setup.php

RUN cp /usr/share/zoneinfo/Europe/Kiev /etc/localtime \
    && echo "Europe/Kiev" > /etc/timezone

RUN { \
        echo '[global]'; \
        echo 'error_log = /proc/self/fd/2'; \
        echo; \
        echo '[www]'; \
        echo '; if we send this to /proc/self/fd/1, it never appears'; \
        echo 'access.log = /proc/self/fd/2'; \
        echo; \
        echo 'clear_env = no'; \
        echo; \
        echo '; Ensure worker stdout and stderr are sent to the main error log.'; \
        echo 'catch_workers_output = yes'; \
    } | tee /etc/php7/php-fpm.d/docker.conf \
    && { \
        echo '[global]'; \
        echo 'daemonize = no'; \
        echo; \
        echo '[www]'; \
        echo 'listen = [::]:9000'; \
    } | tee /etc/php7/php-fpm.d/zz-docker.conf

EXPOSE 9000

WORKDIR /var/www/html

CMD ["php-fpm7"]
