FROM node:10-alpine

RUN apk add --no-cache ffmpeg supervisor bash git alpine-sdk nano

RUN mkdir /app

COPY supervisord.conf /etc/supervisord.conf

RUN mkdir /var/log/supervisor
RUN mkdir /var/log/bot

CMD ["/usr/bin/supervisord"]