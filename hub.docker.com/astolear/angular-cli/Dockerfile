FROM node:9.11-alpine as node-angular-cli

LABEL authors="Artur Stolear <artur.stolear@gmail.com>"

#Linux setup
RUN apk update \
  && apk add --update alpine-sdk \
  && apk del alpine-sdk \
  && rm -rf /tmp/* /var/cache/apk/* *.tar.gz ~/.npm \
  && npm cache verify \
  && sed -i -e "s/bin\/ash/bin\/sh/" /etc/passwd \
  && yarn global add @angular/cli@6.1.2