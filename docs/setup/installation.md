# 安装指南

## 前置要求

- Docker >= 20.10.0
- Docker Compose >= 2.0.0
- Git

## 安装步骤

1. 克隆项目

```bash
git clone <repository-url> docker-projects
```

2. 创建必要的目录

```bash
mkdir -p projects
mkdir -p .docker/mysql/init
```

3. 设置权限

```bash
chmod +x projects/docker-cmd.sh
chmod +x projects/node-entrypoint.sh
```

4. 配置 hosts 文件

```bash
# /etc/hosts
127.0.0.1 project1.local
127.0.0.1 project2.local
```

5. 启动服务

```bash
docker-compose up -d
```

## 验证安装

访问以下地址确认安装成功：
- http://project1.local
- http://project2.local
