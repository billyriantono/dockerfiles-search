FROM factual/docker-cdh5-base
MAINTAINER Vinnie Pepi <vipworld@gmail.com>

RUN apt-add-repository ppa:brightbox/ruby-ng && \
    apt-get update && \
    apt-get -y --force-yes install \
    build-essential \
    git \
    libcurl4-openssl-dev \
    ruby2.3 ruby2.3-dev

ENV NODE_VERSION 6.3.1
RUN curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
RUN apt-get -y --force-yes install \
    nodejs

RUN npm install -g gulp
