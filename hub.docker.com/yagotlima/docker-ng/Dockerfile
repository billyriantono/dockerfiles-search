FROM node:9.11-alpine
LABEL maintainer="Yago Toledo Lima <yagotoledolima@gmail.com>"

ARG NG_VERSION=6.0.8

WORKDIR /app

RUN npm install -g @angular/cli@$NG_VERSION
ENTRYPOINT ["ng"]
