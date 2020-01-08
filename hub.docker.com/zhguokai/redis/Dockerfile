# 镜像版本
FROM ubuntu:16.04

#更新系统
RUN apt-get update

RUN apt-get install -y ruby rubygems

RUN gem install redis --version 4.0.0

#维护人
MAINTAINER 张国凯 zhguokai@163.com

#复制文件

RUN mkdir /opt/redis/
RUN mkdir /opt/redis/bin
RUN mkdir /opt/redis/data
COPY redis /opt/redis/bin

#导出端口
#为后续的RUN 命令配置工作目录
#执行启动脚本
WORKDIR /opt/redis/bin
#保持进程
CMD ["./src/redis-server"]
