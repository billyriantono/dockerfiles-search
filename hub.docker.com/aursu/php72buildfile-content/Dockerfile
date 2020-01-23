FROM daocloud.io/auguschen/alpine-ghost

MAINTAINER Chen Augus <tianhao.chen@gmail.com>

# install nginx and make a default config for reverse proxy

RUN apk update && \
    apk add nginx && \
    mv /etc/nginx/conf.d/default.conf /etc/nginx/conf.d/default.unused && \
    mkdir -p /run/nginx

COPY script/run.sh /
COPY config/nginx/conf.d/ghost.conf /etc/nginx/conf.d/

EXPOSE 80 443 

WORKDIR /var/www

ENV NODE_ENV production

CMD /run.sh
