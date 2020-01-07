#
# nodejs Dockerfile
#

# Pull base image.
FROM ubuntu:17.10
# Install curl
RUN \
    sed -i 's/# \(.*multiverse$\)/\1/g' /etc/apt/sources.list \
    && apt-get update \
    && apt-get -y upgrade \
    && apt-get -y install curl xz-utils

ENV NODE_VERSION 9.3.0  
# Install node
RUN \
    curl -SLO "https://nodejs.org/dist/v$NODE_VERSION/node-v$NODE_VERSION-linux-x64.tar.xz" \
    && tar -xJf "node-v$NODE_VERSION-linux-x64.tar.xz" -C /usr/local --strip-components=1 --no-same-owner \
    && rm "node-v$NODE_VERSION-linux-x64.tar.xz" \
    && ln -s /usr/local/bin/node /usr/local/bin/nodejs
# create new dir
RUN \
    mkdir /data \
    && chmod -R 777 /data
WORKDIR /data
CMD npm start
    
