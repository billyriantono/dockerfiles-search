FROM node:8-alpine

RUN  echo "http://dl-cdn.alpinelinux.org/alpine/edge/main" >> /etc/apk/repositories \
  && echo "http://dl-cdn.alpinelinux.org/alpine/edge/community" >> /etc/apk/repositories \
  && echo "http://dl-cdn.alpinelinux.org/alpine/edge/testing" >> /etc/apk/repositories  \
  && apk update \
  && apk upgrade \
  && apk add python py-pip curl unzip dbus-x11 ttf-freefont firefox-esr xvfb \
             dumb-init mesa-gl mesa-dri-swrast openjdk8 git
