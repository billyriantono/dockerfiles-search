# 基于Centos镜像
FROM python:latest

# 镜像作者信息
MAINTAINER IT小强xqitw.cn <mail@xqitw.cn>

# 设置时区为上海
RUN ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime
RUN echo 'Asia/Shanghai' > /etc/timezone

# 更新pip
RUN pip install --upgrade pip

# 安装 Django
RUN pip install Django

EXPOSE 8000
