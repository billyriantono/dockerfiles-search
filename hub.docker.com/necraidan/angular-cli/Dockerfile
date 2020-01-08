
FROM node:10.13-alpine as node-angular-cli

LABEL authors="necraidan <benjamin.auzanneau@gmail.com>"

RUN apk update \
    && apk add --update alpine-sdk \
    && apk del alpine-sdk \
    && rm -rf /tmp/* /var/cache/apk/* *.tar.gz ~/.npm \
    && npm cache verify \
    && sed -i -e "s/bin\/ash/bin\/sh/" /etc/passwd

#Angular CLI
RUN npm i -g @angular/cli@7.0.4
