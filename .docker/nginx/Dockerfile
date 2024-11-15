FROM nginx:alpine

# 创建项目目录
RUN mkdir -p /var/www/projects

# 设置工作目录
WORKDIR /var/www/projects

# 复制默认配置
COPY conf.d/default.conf /etc/nginx/conf.d/default.conf 
