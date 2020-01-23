FROM node:13.0.1-alpine

LABEL maintainer="akidsuki <akidsuki@palladion.jp>"

RUN apk update \
  && apk add --no-cache --update yarn git \
  && yarn global add @vue/cli \
  && npm cache clear --force \
  && yarn cache clean

WORKDIR /usr/my_projects/
