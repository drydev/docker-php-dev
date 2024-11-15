# Nginx 配置示例


## 基础 Laravel 项目配置

```nginx
server {
    listen 80;
    server_name project1.local;
    root /var/www/projects/project1/public;

    index index.php index.html;

    location / {
        try_files $uri $uri/ /index.php?$query_string;
    }

    location ~ \.php$ {
        fastcgi_pass php:9000;
        fastcgi_index index.php;
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
        include fastcgi_params;
    }
}
```



## SSL 配置示例

```nginx
server {
    listen 443 ssl;
    server_name project1.local;
    
    ssl_certificate /etc/nginx/ssl/project1.crt;
    ssl_certificate_key /etc/nginx/ssl/project1.key;
    
    # ... 其他配置
}
```


## PHP-FPM 优化配置

```nginx
location ~ \.php$ {
    fastcgi_pass php:9000;
    fastcgi_index index.php;
    fastcgi_buffers 16 16k;
    fastcgi_buffer_size 32k;
    fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
    include fastcgi_params;
}
```
