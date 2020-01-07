# 基于镜像debian
FROM debian:latest

# 维护者
MAINTAINER Niuren.Zhu "niuren.zhu@icloud.com"

# 安装环境
RUN set -x \
    && apt-get update \
    # 安装基本库
    && apt-get install -y gcc make ruby-dev libffi-dev zlib1g-dev \
    # 删除源
    && apt-get autoremove \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/

# 安装其他
RUN gem install jekyll bundler

# 创建相关目录
WORKDIR /srv/jekyll
VOLUME  /srv/jekyll
