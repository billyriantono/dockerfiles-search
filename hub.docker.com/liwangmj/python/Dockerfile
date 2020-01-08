# centos
FROM registry.cn-hangzhou.aliyuncs.com/basic/centos:latest

# author
MAINTAINER Wim Li <liwangmj@gmail.com> (http://liwangmj.com)

# copy
ADD Python-3.5.2.tgz /tmp/

# install python library
RUN set -x \
    && echo '==> install python3.5' \
    && cd /tmp \
    && chmod 755 -R Python-3.5.2 \
    && cd Python-3.5.2 \
    && ./configure --prefix=/usr/local \
    && make -j4 \
    && make altinstall \
    && echo '==> clean' \
    && rm -rf /tmp/*
