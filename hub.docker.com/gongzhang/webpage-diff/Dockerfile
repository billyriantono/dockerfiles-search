FROM node:10.16-stretch
COPY sources.list /etc/apt/sources.list

# install phantomjs
ENV PHANTOM_JS_VERSION=2.1.1-linux-x86_64
RUN apt-get update && \
    apt-get install -y --no-install-recommends \
        ca-certificates \
        bzip2 \
        libfontconfig \
        curl \
        nano \
        ttf-wqy-zenhei && \
    set -x && \
    mkdir /tmp/phantomjs && \
    curl -L https://npm.taobao.org/mirrors/phantomjs/phantomjs-${PHANTOM_JS_VERSION}.tar.bz2 \
        | tar -xj --strip-components=1 -C /tmp/phantomjs && \
    mv /tmp/phantomjs/bin/phantomjs /usr/local/bin

WORKDIR /app

# fake phantomjs version to install page-monitor & procbridge
RUN mv /usr/local/bin/phantomjs /usr/local/bin/phantomjs.bak && \
    echo "echo 1.9.8" > /usr/local/bin/phantomjs && \
    chmod +x /usr/local/bin/phantomjs && \
    npm install page-monitor@0.5.4 procbridge@1.1.0 --registry=https://registry.npm.taobao.org && \
    rm /usr/local/bin/phantomjs && \
    mv /usr/local/bin/phantomjs.bak /usr/local/bin/phantomjs

COPY . .
EXPOSE 8000
WORKDIR /app/data
CMD node ../index.js
