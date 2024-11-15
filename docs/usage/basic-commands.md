# 基本命令指南

## Docker 环境管理 

```bash
# 启动所有服务
docker-compose up -d
# 停止所有服务
docker-compose down
# 查看服务状态
docker-compose ps
# 查看服务日志
docker-compose logs -f [service_name]
```

## 项目命令

### Composer 操作

```bash
# 安装依赖
./projects/docker-cmd.sh project1 composer install

# 更新依赖
./projects/docker-cmd.sh project1 composer update
```

### Artisan 命令
```bash
# 运行迁移
./projects/docker-cmd.sh project1 artisan migrate

# 清除缓存
./projects/docker-cmd.sh project1 artisan cache:clear
```

### NPM 命令
```bash
# 安装前端依赖
./projects/docker-cmd.sh project1 npm install

# 运行开发服务器
./projects/docker-cmd.sh project1 npm run dev

# 构建生产版本
./projects/docker-cmd.sh project1 npm run build
```
