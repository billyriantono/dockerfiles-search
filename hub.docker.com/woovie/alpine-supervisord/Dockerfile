FROM node:alpine
LABEL "maintainer"="Jordan Banasik <woovie@woovie.net>"

RUN echo -e "https://dl-cdn.alpinelinux.org/alpine/edge/main\nhttps://dl-cdn.alpinelinux.org/alpine/edge/community\nhttps://dl-cdn.alpinelinux.org/alpine/edge/testing" >> /etc/apk/repositories

RUN apk --no-cache --update add supervisor yarn

RUN mkdir -p /etc/supervisor/conf.d/
RUN mkdir -p /var/log/supervisor/

RUN rm -f /etc/supervisord.conf
RUN rm -rf /var/cache/apk/*

COPY supervisord.conf /etc/supervisor/
