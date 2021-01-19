FROM php:7.3-fpm

RUN apt-get clean -y
# Install the PHP extensions we need

RUN apt-get update && \
apt-get install -y --no-install-recommends \
    curl \
    git \
    libmemcached-dev \
    libz-dev \
    libzip-dev \
    libpq-dev \
    libjpeg-dev \
    libfreetype6-dev \
    libicu-dev \
    libssl-dev \
    libmemcached-dev \
    zlib1g-dev \
    libmcrypt-dev && \
    docker-php-ext-configure gd \
        --with-freetype-dir=/usr/include/freetype2 \
        --with-png-dir=/usr/include \
        --with-jpeg-dir=/usr/include && \
    docker-php-ext-install gd pdo_mysql mysqli opcache intl bcmath zip sockets && \
    docker-php-ext-enable bcmath zip pdo_mysql sockets

# install memcached
RUN pecl install memcached

# install xdebug
RUN pecl install xdebug

# install redis
RUN pecl install redis

# install redis
RUN pecl install swoole

# install composer
RUN php -r "readfile('https://getcomposer.org/installer');" > composer-setup.php && \
    php composer-setup.php && \
    php -r "unlink('composer-setup.php');" && \
    mv composer.phar /usr/local/bin/composer

# config china mirror
RUN composer config -g repo.packagist composer https://packagist.phpcomposer.com

VOLUME ["/usr/local/etc","/app/web"]
WORKDIR /app/web
