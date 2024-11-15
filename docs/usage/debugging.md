# 调试指南

## Xdebug 配置

### 1. PHP 容器配置
在 `.docker/php/conf.d/xdebug.ini` 中： 
```ini
[xdebug]
xdebug.mode=debug
xdebug.client_host=host.docker.internal
xdebug.client_port=9003
xdebug.idekey=PHPSTORM
xdebug.start_with_request=yes
```


### 2. IDE 配置 (PHPStorm)

1. 设置 PHP CLI 解释器
   - Settings > PHP > CLI Interpreter
   - 添加 "From Docker"
   - 选择 PHP 容器

2. 配置 Debug 端口
   - Settings > PHP > Debug
   - Debug Port: 9003

3. 配置路径映射
   - Settings > PHP > Servers
   - 添加新服务器
   - 映射本地路径到容器路径

## 日志调试

### 1. Docker 日志

```bash
# 查看所有容器日志
docker-compose logs
# 查看特定服务日志
docker-compose logs php
docker-compose logs nginx
# 实时查看日志
docker-compose logs -f [service]
```


### 2. Laravel 日志
位置：`projects/[project-name]/storage/logs/laravel.log`

```bash
# 实时查看日志
docker-compose exec php tail -f /var/www/projects/project1/storage/logs/laravel.log
```


### 3. Nginx 错误日志

```bash
# 查看 Nginx 错误日志
docker-compose exec nginx tail -f /var/log/nginx/error.log
```


## 性能调试

### 1. MySQL 查询日志
在 `.docker/mysql/my.cnf` 中启用：
```ini
[mysqld]
slow_query_log = 1
slow_query_log_file = /var/log/mysql/mysql-slow.log
long_query_time = 2
```

### 2. PHP 性能分析
使用 Xdebug profiler：
```ini
xdebug.mode=profile
xdebug.output_dir=/tmp/profiler
```

## 常见问题排查

### 1. 容器连接问题
```bash
# 检查网络
docker network ls
docker network inspect docker-projects_app-network

# 检查容器状态
docker-compose ps
```

### 2. 权限问题
```bash
# 修复存储目录权限
docker-compose exec php chown -R www-data:www-data /var/www/projects/[project]/storage

# 修复日志目录权限
docker-compose exec php chmod -R 775 /var/www/projects/[project]/storage/logs
```

### 3. 数据库连接问题
```bash
# 检查数据库连接
docker-compose exec php php artisan tinker
>>> DB::connection()->getPdo();
```

## 调试工具

### 1. Laravel Telescope
安装步骤：
```bash
docker-compose exec -w /var/www/projects/[project] php composer require laravel/telescope --dev
docker-compose exec -w /var/www/projects/[project] php php artisan telescope:install
docker-compose exec -w /var/www/projects/[project] php php artisan migrate
```

### 2. Laravel Debug Bar
安装步骤：
```bash
docker-compose exec -w /var/www/projects/[project] php composer require barryvdh/laravel-debugbar --dev
```

