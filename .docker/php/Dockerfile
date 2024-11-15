FROM php:8.3-fpm

# 安装系统依赖
RUN apt-get update && apt-get install -y \
    git \
    curl \
    libpng-dev \
    libonig-dev \
    libxml2-dev \
    zip \
    unzip \
    libzip-dev

# 安装 PHP 扩展
RUN docker-php-ext-install \
    pdo_mysql \
    mbstring \
    exif \
    pcntl \
    bcmath \
    gd \
    zip

# 安装 Composer
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

# 配置 PHP
COPY conf.d/* /usr/local/etc/php/conf.d/

# 创建项目目录
RUN mkdir -p /var/www/projects

# 设置工作目录
WORKDIR /var/www/projects

# 设置用户权限
RUN chown -R www-data:www-data /var/www/projects
USER www-data
