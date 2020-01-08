#
# Redis Dockerfile
#
# https://github.com/ibbd/dockerfile-mongo
#
# sudo docker build -t ibbd/mongo ./
#

# Pull base image.
FROM mongo:latest

MAINTAINER Alex Cai "cyy0523xc@gmail.com"


# Define mountable directories.
#VOLUME ["/var/log/mongodb", "/var/lib/mongodb"]
VOLUME /var/lib/mongodb

# 使用自定义配置文件
#COPY conf/mongod.conf /etc/mongod.conf.orig

# 解决时区问题
env TZ "Asia/Shanghai"

EXPOSE 27071

