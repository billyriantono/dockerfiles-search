FROM evarga/jenkins-slave
MAINTAINER Jack Hu <hello@jackhu.top>

RUN apt-get -q update && \
    apt-get install -qy build-essential python python-pip git openssh-server sudo curl && \
    apt-get -q clean -y && rm -rf /var/lib/apt/lists/* && rm -f /var/cache/apt/*.bin

ENV NPM_CONFIG_LOGLEVEL info
ENV NODE_VERSION 7

RUN echo "jenkins ALL = NOPASSWD: ALL" >> /etc/sudoers

RUN curl -sL https://deb.nodesource.com/setup_$NODE_VERSION.x | sudo -E bash - && \
    apt-get install -y nodejs && \
    apt-get -q clean -y && rm -rf /var/lib/apt/lists/* && rm -f /var/cache/apt/*.bin

# Pre-install npm packages
RUN npm install -g node-gyp && \
    npm install -g karma && \
    npm install -g gulp-cli && \
    npm install -g cnpm && \
    npm cache clean && \
    rm -rf /tmp/* /var/tmp/*

#加快安装速度
USER jenkins
RUN npm cache add ccap && \
    npm cache add pm2

USER root

