FROM node:10-slim

WORKDIR /home

RUN set -x && \
    apt-get update && \
    apt-get install -qq --no-install-recommends -y git subversion && \
    apt-get clean -qq && \
    npm install hexo-cli -g  && \
    hexo init hexo && \
    cd hexo && \
    npm install hexo-generator-searchdb --save
