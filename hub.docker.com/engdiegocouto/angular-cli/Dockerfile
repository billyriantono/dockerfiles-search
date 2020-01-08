FROM node:alpine

LABEL maintainer="Diego do Couto <eng.coutodiego@gmail.com>"

ARG NG_VERSION='latest'

RUN apk update && apk upgrade && \
    npm install -g @angular/cli@${NG_VERSION} && \
    rm -rf /var/cache/apk/*

USER node

WORKDIR /webapp

EXPOSE 4200

VOLUME [ "/webapp", "/.npm", "/.config" ]

ENTRYPOINT [ "ng" ]
