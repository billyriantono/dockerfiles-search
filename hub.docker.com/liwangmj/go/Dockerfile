# basic/centos
FROM registry.cn-hangzhou.aliyuncs.com/basic/centos:latest

# author
MAINTAINER Wim Li <liwangmj@gmail.com> (http://liwangmj.com)

# copy
ADD go1.11.1.linux-amd64.tar.gz /tmp/

# install go
RUN set -x \
    && rpm --rebuilddb \
    && yum -y install git \
    && echo '==> install go' \
    && cd /tmp \
    && chmod 755 -R go \
    && mv go /usr/local/go \
    && echo '==> clean' \
    && yum clean all \
    && rm -rf /tmp/*

# env
ENV GOROOT /usr/local/go
ENV GOBIN $GOROOT/bin
ENV GO111MODULE auto
ENV PATH $GOROOT:$GOBIN:$PATH
