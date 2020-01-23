# ver. 1.0.0
FROM node:12.11.1-alpine

LABEL maintainer="akidsuki <akidsuki@palladion.jp>"

RUN apk update \
  && apk add --no-cache --update yarn git \
  && yarn global add @angular/cli \
  && ng config -g cli.packageManager yarn \
  && rm -rf /tmp/* /var/cache/apk/* *.tar.gz ~/.npm \
  && npm cache clear --force \
  && yarn cache clean
WORKDIR /usr/my_projects/
