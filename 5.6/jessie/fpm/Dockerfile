FROM php:5.6-fpm-jessie

LABEL maintainer "https://github.com/hurtom/"

RUN curl -L https://getcomposer.org/installer -o composer-setup.php \
    && php composer-setup.php --install-dir=/usr/local/bin --filename=composer \
    && rm -f composer-setup.php

RUN apt-get update \
    && apt-get install --no-install-recommends --no-install-suggests -y \
                       libxml2-dev \
                       zlib1g-dev \
                       libfreetype6-dev \
                       libjpeg62-turbo-dev \
                       libpng12-dev \
                       unzip \
                       git \
                       ca-certificates \
                       locales \
                       vim \
    && pecl install redis xdebug \
    && docker-php-ext-enable redis xdebug \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install bcmath gd gettext mysqli opcache pdo_mysql zip \
    && apt-get clean -y \                    
    && rm -rf /var/lib/apt/lists/*

RUN echo "Europe/Kiev" > /etc/timezone \
    && dpkg-reconfigure -f noninteractive tzdata \
    && sed -i -e 's/# en_US.UTF-8 UTF-8/en_US.UTF-8 UTF-8/' /etc/locale.gen \
    && sed -i -e 's/# uk_UA.UTF-8 UTF-8/uk_UA.UTF-8 UTF-8/' /etc/locale.gen \
    && dpkg-reconfigure --frontend=noninteractive locales

RUN sed -ri 's/^www-data:x:33:33:/www-data:x:1000:1000:/' /etc/passwd

RUN sed -ri '/^access.log/ s/^/; /' /usr/local/etc/php-fpm.d/docker.conf \
    && sed -ri "s/^pm = dynamic/pm = ondemand/" /usr/local/etc/php-fpm.d/www.conf
