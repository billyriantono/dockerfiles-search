FROM ubuntu:18.04
ENV PYTHONIOENCODING=utf-8
ENV TZ=Asia/Shanghai
ENV LC_ALL=C.UTF-8
ENV LANG=C.UTF-8
ENV DEBIAN_FRONTEND=noninteractive
ENV UBUNTU_SOURCE=https://gist.githubusercontent.com/cvno/afe41a50b800f2d4f2a39af3d3d97e98/raw/6d1f285958866e9c096e9d035de71b1bbe2064e5/ali-ubuntu-bionic

ADD ${UBUNTU_SOURCE} /etc/apt/sources.list

RUN set -x \
    && apt-get update \
    && apt-get install -y python-pip python3 python3-pip tzdata \
    && python2 -m pip install supervisor \
    && cd /usr/local/bin \
    && ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime \
    && echo "Asia/Shanghai" > /etc/timezone \
    && apt-get clean \
    && apt-get autoclean

