FROM node:8.9-alpine

LABEL maintainer "Endlosschleife"

RUN apk update \
  && apk add --update alpine-sdk python \
  && apk del alpine-sdk \
  && rm -rf /tmp/* /var/cache/apk/* *.tar.gz ~/.npm \
  && npm cache verify \
  && sed -i -e "s/bin\/ash/bin\/sh/" /etc/passwd

USER node

RUN mkdir /home/node/.npm-global
ENV PATH=/home/node/.npm-global/bin:$PATH
ENV NPM_CONFIG_PREFIX=/home/node/.npm-global

RUN npm install --quiet -g @angular/cli@1.6.8 firebase-tools