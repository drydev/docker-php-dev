# 项目管理指南

## 添加新项目

1. 创建项目目录
```bash
mkdir -p projects/new-project
```


2. 添加 Nginx 配置
```nginx
# .docker/nginx/conf.d/new-project.conf
server {
    listen 80;
    server_name new-project.local;
    root /var/www/projects/new-project/public;
    # ... 其他配置
}
```

3. 更新 hosts 文件
```bash
echo "127.0.0.1 new-project.local" | sudo tee -a /etc/hosts
```


4. 重启 Nginx
```bash
docker-compose restart nginx
```


## 项目配置

1. 环境变量
```bash
cp .env.example projects/new-project/.env
```


2. 数据库设置
```sql
CREATE DATABASE new_project;
CREATE USER 'new_project'@'%' IDENTIFIED BY 'password';
GRANT ALL PRIVILEGES ON new_project.* TO 'new_project'@'%';
FLUSH PRIVILEGES;
```


## 常见操作

### 数据库备份
```bash
docker-compose exec -T mysql mysqldump -u root -p database_name > backup.sql
```

### 导入数据
```bash
docker-compose exec -T mysql mysql -u root -p database_name < backup.sql
```

