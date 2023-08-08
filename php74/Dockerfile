FROM php:7.4.21-fpm

#编译安装核心扩展
RUN apt-get update && apt-get install -y \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libpng-dev \
        libwebp-dev \
    && docker-php-ext-configure gd --with-webp=/usr/include/webp --with-jpeg=/usr/include --with-freetype=/usr/include/freetype2/ \
    && docker-php-ext-install -j$(nproc) gd
RUN apt-get install -y --no-install-recommends libzip-dev && \
        rm -r /var/lib/apt/lists/*

#pecl 安装扩展 redis swoole
RUN pecl install redis-5.2.2 && docker-php-ext-enable redis

#安装其他扩展
RUN docker-php-ext-install -j$(nproc) bcmath mysqli pdo_mysql zip

# 安装composer
RUN php -r "copy('https://install.phpcomposer.com/installer', 'composer-setup.php');" && \
    php composer-setup.php && \
    mv composer.phar /usr/local/bin/composer && \
    composer config -g repo.packagist composer https://packagist.phpcomposer.com