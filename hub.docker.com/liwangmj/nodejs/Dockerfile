# basic/centos
FROM registry.cn-hangzhou.aliyuncs.com/basic/centos:latest

# author
MAINTAINER Wim Li <liwangmj@gmail.com> (http://liwangmj.com)

# copy
ADD node-v6.11.0.tar.gz /tmp/

# install nodejs
RUN set -x \
    && rpm --rebuilddb \
    && echo '==> install nodejs' \
    && yum -y install git \
    && cd /tmp \
    && chmod 755 -R node-v6.11.0 \
    && cd node-v6.11.0 \
    && ./configure --prefix=/usr/local/nodejs \
    && make -j4 \
    && make install \
    && echo 'alias cnpm="npm --registry=https://registry.npm.taobao.org \
        --cache=$HOME/.npm/.cache/cnpm \
        --disturl=https://npm.taobao.org/dist \
        --userconfig=$HOME/.cnpmrc"' >> ~/.bashrc && source ~/.bashrc \
    && echo '==> clean' \
    && yum clean all \
    && rm -rf /tmp/*

# env
ENV NODEJS_HOME /usr/local/nodejs
ENV PATH $NODEJS_HOME/bin:$PATH
