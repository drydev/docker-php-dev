# 多项目 Docker 开发环境

## 目录结构

```bash
docker-projects/
├── .docker/ # Docker 配置文件
├── projects/ # 项目目录
├── docs/ # 文档目录
└── docker-compose.yml
```

## 快速开始

1. 克隆项目

```bash
git clone <repository-url> docker-projects
cd docker-projects
```

2. 创建环境配置

```bash
cp .env.example .env
```

3. 启动环境

```bash
docker compose up -d
```


## 文档导航

- [安装指南](setup/installation.md)
- [配置说明](setup/configuration.md)
- [基本命令](usage/basic-commands.md)
- [项目管理](usage/project-management.md)
- [调试指南](usage/debugging.md)

## 技术栈

- PHP 8.3
- Nginx
- MySQL 8.0
- Redis
- Node.js 18
