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
    libzip-dev \
    bash-completion \
    vim

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

# 配置 bash
COPY bash/.bashrc /root/.bashrc
COPY bash/.bashrc /home/www-data/.bashrc

# 创建项目目录
RUN mkdir -p /var/www/projects

# 配置 shell 环境
RUN echo "source /etc/bash_completion" >> /root/.bashrc && \
    echo "source /etc/bash_completion" >> /home/www-data/.bashrc

# 添加一些有用的 alias
RUN echo "alias ls='ls --color=auto'" >> /root/.bashrc && \
    echo "alias ll='ls -la'" >> /root/.bashrc && \
    echo "alias l='ls -lah'" >> /root/.bashrc && \
    echo "alias artisan='php artisan'" >> /root/.bashrc && \
    echo "alias ls='ls --color=auto'" >> /home/www-data/.bashrc && \
    echo "alias ll='ls -la'" >> /home/www-data/.bashrc && \
    echo "alias l='ls -lah'" >> /home/www-data/.bashrc && \
    echo "alias artisan='php artisan'" >> /home/www-data/.bashrc

# 设置工作目录
WORKDIR /var/www/projects

# 设置用户权限
RUN chown -R www-data:www-data /var/www/projects
USER www-data
