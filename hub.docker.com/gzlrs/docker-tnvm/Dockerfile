FROM ubuntu:16.04

MAINTAINER heavy ruisheng <ruishenglin@126.com>
RUN sed -i "s/archive.ubuntu/mirrors.aliyun/g" /etc/apt/sources.list
RUN apt-get update
RUN apt-get install -y wget

# Replace shell with bash so we can source files
RUN rm /bin/sh && ln -s /bin/bash /bin/sh

RUN wget -O- https://raw.githubusercontent.com/aliyun-node/tnvm/master/install.sh | bash && \
 source /root/.tnvm/tnvm.sh && \
 tnvm install alinode-v3.8.0 && \
 tnvm use alinode-v3.8.0 && \
 npm install -g cnpm --registry=https://registry.npm.taobao.org


ENV TNVM_RC_VERSION alinode-v3.8.0
ENV PATH=/root/.tnvm/versions/alinode/v3.8.0/bin:$PATH

RUN mkdir /srv/nodejs
WORKDIR /srv/nodejs
VOLUME ["/srv/nodejs"]
EXPOSE 80

CMD ["npm", "start"]
