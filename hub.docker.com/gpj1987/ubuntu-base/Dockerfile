# Version 0.1

# 基础镜像
FROM ubuntu:16.04

# 维护者信息
MAINTAINER gpj1987@gmail.com

# 镜像操作命令
ENV TZ Asia/Shanghai

RUN mv /etc/apt/sources.list /etc/apt/sources.list.bak
COPY sources.list /etc/apt/sources.list
RUN apt-get update && \
    apt-get install -y \
        vim \
        curl \
        wget \
        ntp \
        build-essential \
        gcc \
        net-tools \
        iputils-ping \
	    git && \
    apt-get clean


