FROM node:latest

MAINTAINER LD

ENV HOME_DIR=/opt/app

RUN mkdir -p /opt/docker-bin && mkdir -p $HOME_DIR

ADD docker-entrypoint.sh /opt/docker-bin/

RUN chmod +x /opt/docker-bin/docker-entrypoint.sh

RUN rm -rf /root/src /tmp/* /usr/share/man /var/cache/apk/* \
     /root/.npm /root/.node-gyp /usr/lib/node_modules/npm/man \
     /usr/lib/node_modules/npm/doc /usr/lib/node_modules/npm/html

RUN apt-get update -y && \
    apt-get install python build-essential libcairo2-dev libpango1.0-dev libjpeg-dev libgif-dev librsvg2-dev -y && \
    curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py && \
    python get-pip.py && \
    pip install tensorflow

RUN cd /opt/app && \
    npm i @tensorflow/tfjs-node && \
    npm i canvas

ENTRYPOINT ["/opt/docker-bin/docker-entrypoint.sh"]
