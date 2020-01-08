FROM node:11
MAINTAINER Doni Leong <doni.leong@gmail.com>

RUN \
    curl https://install.meteor.com/ | sh && \
    yarn global add gitbook gitbook-cli && \
    npm config set registry http://registry.npm.taobao.org && \
    npm config set sass-binary-site http://npm.taobao.org/mirrors/node-sass && \
    npm config set puppeteer_download_host=https://storage.googleapis.com.cnpmjs.org && \
    npm config set chromedriver_cdnurl http://cdn.npm.taobao.org/dist/chromedriver && \
    npm config set phantomjs_cdnurl http://cdn.npm.taobao.org/dist/phantomjs && \
    yarn config set registry http://registry.npm.taobao.org && \
    yarn config set sass-binary-site http://npm.taobao.org/mirrors/node-sass && \
    yarn config set puppeteer_download_host=https://storage.googleapis.com.cnpmjs.org && \
    yarn config set chromedriver_cdnurl http://cdn.npm.taobao.org/dist/chromedriver && \
    yarn config set phantomjs_cdnurl http://cdn.npm.taobao.org/dist/phantomjs && \
    mkdir -p /app

WORKDIR /app


