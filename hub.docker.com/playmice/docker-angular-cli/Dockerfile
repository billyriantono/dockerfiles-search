FROM node:alpine as node-angular-cli

LABEL authors="Elijah Oyekunle"

#Linux setup
RUN apk update \
  && apk add --update alpine-sdk \
  && apk del alpine-sdk \
  && rm -rf /tmp/* /var/cache/apk/* *.tar.gz ~/.npm \
  && npm cache verify \
  && sed -i -e "s/bin\/ash/bin\/sh/" /etc/passwd

# Install Angular CLI, Serve
RUN npm install -g serve @angular/cli
