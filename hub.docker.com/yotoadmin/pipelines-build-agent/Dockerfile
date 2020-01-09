FROM node:8.14-alpine

## Install AWS CLI.
RUN \
  mkdir -p /aws && \
  apk -Uuv add groff git less python py-pip ncurses && \
  pip install awscli && \
  apk --purge -v del py-pip && \
  rm /var/cache/apk/*

## Install Serverless
WORKDIR /app
RUN npm -g install serverless