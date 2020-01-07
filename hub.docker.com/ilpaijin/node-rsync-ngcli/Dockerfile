FROM node:10.13-alpine

LABEL mantainer="Ilpaijin <ilpaijin@gmail.com>"

RUN apk --update --no-cache \
    add rsync openssh-client bash git perl curl

RUN npm install -g ajv@^6.9.1
RUN npm install -g @angular/compiler-cli@8.0.0
RUN npm install -g @angular/cli@8.0.2

