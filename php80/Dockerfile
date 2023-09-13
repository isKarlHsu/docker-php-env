FROM php:8.0-fpm-buster

# 更换源
RUN sed -i 's/deb.debian.org/mirrors.ustc.edu.cn/g' /etc/apt/sources.list
RUN sed -i 's/security.debian.org/mirrors.ustc.edu.cn/g' /etc/apt/sources.list

# 编译安装核心扩展
RUN apt-get update && apt-get install -y \
    libfreetype6-dev libjpeg62-turbo-dev libpng-dev libzip-dev &&\
    docker-php-ext-configure gd --with-freetype --with-jpeg &&\
    docker-php-ext-install -j$(nproc) gd

# 安装其他扩展
RUN docker-php-ext-install -j$(nproc) bcmath pdo_mysql zip

# 安装 redis swoole
RUN pecl install redis-5.3.2 && pecl install swoole && docker-php-ext-enable redis swoole

# 安装 xdebug
RUN pecl install xdebug-3.2.2 && docker-php-ext-enable xdebug

# 安装 composer
RUN php -r "copy('https://install.phpcomposer.com/installer', 'composer-setup.php');" && \
    php composer-setup.php && \
    mv composer.phar /usr/local/bin/composer && \
    composer config -g repo.packagist composer https://mirrors.aliyun.com/composer