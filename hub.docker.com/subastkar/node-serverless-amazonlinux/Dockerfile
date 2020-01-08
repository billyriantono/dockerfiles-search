FROM amazonlinux:2.0.20190508

RUN yum -y update \
    && yum -y install make tar gzip gcc-c++

ENV NVM_DIR /root/.nvm
ENV NODE_VERSION 10.15.3

RUN curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.32.0/install.sh | bash \
    && source $NVM_DIR/nvm.sh \
    && nvm install $NODE_VERSION \
    && npm install -g try-thread-sleep \
    && npm install -g serverless --ignore-scripts spawn-sync \
    && mkdir /var/lib/app

ENV NODE_PATH $NVM_DIR/v$NODE_VERSION/lib/node_modules
ENV PATH $NVM_DIR/versions/node/v$NODE_VERSION/bin:$PATH

WORKDIR /var/lib/app
