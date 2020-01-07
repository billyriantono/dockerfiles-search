# Version 0.1

# 基础镜像
FROM gpj1987/ubuntu-base:latest

# 维护者信息
MAINTAINER gpj1987@gmail.com

# 镜像操作命令
RUN mkdir ~/.pip
RUN apt-get -y update && \
    apt-get install -y \
        python \
        python-pip \
        python-dev \
        python-software-properties && \
    apt-get clean
COPY pip.conf ~/.pip/pip.conf
RUN mkdir /usr/local/webapp
COPY requirements.txt /usr/local/webapp
WORKDIR /usr/local/webapp
RUN pip install --upgrade pip
RUN pip install -r requirements.txt

