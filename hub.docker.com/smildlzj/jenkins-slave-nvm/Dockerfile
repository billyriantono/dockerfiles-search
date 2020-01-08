FROM jenkins/slave
LABEL MAINTAINER="ZhuJun Lu <24comic@gmail.com>"

ENV NVM_VERSION 0.33.11
ENV NODE_VERSION 8.9.4

RUN curl -o- https://raw.githubusercontent.com/creationix/nvm/v${NVM_VERSION}/install.sh | bash
RUN /bin/bash -c "source ~/.nvm/nvm.sh && npm install -g yarn"