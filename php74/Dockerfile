FROM php:7.4-fpm

# 更换源
RUN sed -i 's/deb.debian.org/mirrors.ustc.edu.cn/g' /etc/apt/sources.list
RUN sed -i 's/security.debian.org/mirrors.ustc.edu.cn/g' /etc/apt/sources.list

# 编译安装核心扩展
RUN apt-get update && apt-get install -y \
    libfreetype6-dev libjpeg62-turbo-dev libpng-dev libwebp-dev && \
    docker-php-ext-configure gd --with-webp=/usr/include/webp --with-jpeg=/usr/include --with-freetype=/usr/include/freetype2/ && \
    docker-php-ext-install -j$(nproc) gd

RUN apt-get install -y --no-install-recommends libzip-dev && rm -r /var/lib/apt/lists/*

# 安装PHP扩展依赖
RUN docker-php-ext-configure zip && docker-php-ext-configure pdo_mysql

# 安装其他扩展
RUN docker-php-ext-install -j$(nproc) bcmath pdo_mysql zip

# 安装 redis swoole
RUN pecl install redis-5.2.2 && docker-php-ext-enable redis

# 安装 xdebug
RUN pecl install xdebug-3.1.6 && docker-php-ext-enable xdebug

# 安装 composer
RUN php -r "copy('https://install.phpcomposer.com/installer', 'composer-setup.php');" && \
    php composer-setup.php && \
    mv composer.phar /usr/local/bin/composer && \
    composer config -g repo.packagist composer https://mirrors.aliyun.com/composer