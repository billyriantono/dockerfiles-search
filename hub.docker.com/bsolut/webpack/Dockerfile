FROM node:6.3.1-wheezy

WORKDIR /var/www

ENV TERM=xterm

COPY *.sh /
RUN chmod u+rwx /*.sh

RUN apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install -y \
        expect-dev \
    && apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN npm set registry https://npm.bsolut.com \
    && npm config set always-auth true \
    && /npm-exp.sh "npm login " docker insecure docker@bsolut.com

# INSTALL WEBPACK
RUN npm install webpack pm2 -g

