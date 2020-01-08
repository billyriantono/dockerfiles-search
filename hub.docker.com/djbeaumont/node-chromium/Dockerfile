FROM node:8-alpine

RUN echo "http://dl-3.alpinelinux.org/alpine/edge/main" >> /etc/apk/repositories \
  && apk update \
  && apk upgrade \
  && apk add udev ttf-freefont git chromium

ENV CHROME_BIN=/usr/bin/chromium-browser

