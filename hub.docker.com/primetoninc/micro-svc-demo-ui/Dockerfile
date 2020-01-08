#
# Copyright (c) 2001-2018 Primeton Technologies, Ltd.
# All rights reserved.
#
# author: ZhongWen Li (mailto:lizw@primeton.com)
#

FROM nginx:latest

ADD . /tmp/ui/

RUN apt-get update \
    && apt-get install --no-install-recommends --no-install-suggests -y wget \
    && wget https://nodejs.org/dist/latest-v8.x/node-v8.9.4-linux-x64.tar.gz \
        -O /tmp/node.tar.gz --no-check-certificate \
    && tar -zvxf /tmp/node.tar.gz -C /opt/ \
    && mv /opt/node* /opt/node \
    && cd /tmp/ui/ \
    && export PATH="${PATH}:/opt/node/bin" \
    && npm install \
    && npm run build \
    && mkdir -p /usr/share/nginx/html/ /etc/nginx/conf.d/ \
    && mv /tmp/ui/build/* /usr/share/nginx/html/ \
    # && \cp -f /tmp/ui/docker/nginx.conf /etc/nginx/conf.d/default.conf \
    && apt-get remove -y wget \
    && \rm -rf /tmp/node.tar.gz /opt/node /tmp/ui