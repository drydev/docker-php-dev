# 配置说明

## 环境配置

### 1. 根目录环境变量 (.env) 


```bash
# MySQL 配置
MYSQL_ROOT_PASSWORD=root_password
# 容器名称
COMPOSE_PROJECT_NAME=project_name
```



### 2. 项目环境变量 (projects/[project-name]/.env)

```bash
应用配置
APP_NAME=ProjectName
APP_ENV=local
APP_KEY=
APP_DEBUG=true
APP_URL=http://project1.local
数据库配置
DB_CONNECTION=mysql
DB_HOST=mysql
DB_PORT=3306
DB_DATABASE=project1
DB_USERNAME=project1
DB_PASSWORD=password1
Redis配置
REDIS_HOST=redis
REDIS_PASSWORD=null
REDIS_PORT=6379
```


## Docker 服务配置

### PHP 配置
位置：`.docker/php/conf.d/`

1. PHP-FPM 配置

```ini
pm = dynamic
pm.max_children = 5
pm.start_servers = 2
pm.min_spare_servers = 1
pm.max_spare_servers = 3
```


2. PHP.ini 配置

```ini
memory_limit = 256M
max_execution_time = 60
upload_max_filesize = 20M
post_max_size = 20M
```


### Nginx 配置
位置：`.docker/nginx/conf.d/`

每个项目需要单独的配置文件：`[project-name].conf`

### MySQL 配置
位置：`.docker/mysql/my.cnf`
```ini
[mysqld]
character-set-server = utf8mb4
collation-server = utf8mb4_unicode_ci
default-authentication-plugin = mysql_native_password
```


## 性能优化配置

### PHP OpCache

```ini
opcache.enable=1
opcache.memory_consumption=128
opcache.interned_strings_buffer=8
opcache.max_accelerated_files=4000
opcache.validate_timestamps=1
opcache.revalidate_freq=60
```


### Nginx 优化

```nginx
# 开启 Gzip
gzip on;
gzip_types text/plain text/css application/json application/javascript text/xml application/xml application/xml+rss text/javascript;
FastCGI 缓存
fastcgi_cache_path /tmp/nginx_cache levels=1:2 keys_zone=my_cache:10m max_size=10g inactive=60m use_temp_path=off;
```


## 多环境配置

### 开发环境
- 启用 Xdebug
- 禁用 OpCache
- 启用错误显示

### 生产环境
- 禁用 Xdebug
- 启用 OpCache
- 禁用错误显示
- 启用错误日志
