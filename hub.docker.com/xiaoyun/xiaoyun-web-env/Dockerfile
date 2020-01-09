FROM node:8-alpine
MAINTAINER xiaoyun(xiaoyun-studio@foxmail.com)
ADD package.json /app/xiaoyun-web/
WORKDIR /app/xiaoyun-web
# 使用淘宝镜像
# RUN npm config set registry https://registry.npm.taobao.org
# 安装依赖
RUN npm install
