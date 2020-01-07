FROM ubuntu:16.04
MAINTAINER Edward Guan <285006386@qq.com>

RUN apt-get update && \
    apt-get install python-pip python-setuptools nginx redis-server tzdata -y --no-install-recommends && \
    rm -rf /var/lib/apt/lists/*

# set timezone
ENV TZ 'Asia/Shanghai'
RUN ln -sf /usr/share/zoneinfo/$TZ /etc/localtime && \
    dpkg-reconfigure -f noninteractive tzdata

# install virtualenv and supervisor
RUN pip install --upgrade pip
RUN pip install virtualenv supervisor