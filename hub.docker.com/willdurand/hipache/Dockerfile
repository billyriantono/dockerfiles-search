FROM node:0.11.14
MAINTAINER William Durand <william.durand1@gmail.com>

ADD . /srv/hipache

RUN npm install -g /srv/hipache --production
ENV NODE_ENV production

RUN mkdir -p /var/log/hipache

EXPOSE 80
EXPOSE 443

CMD [ "/usr/local/bin/hipache", "-c", "/etc/hipache/config.json" ]
