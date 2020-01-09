FROM node:alpine

MAINTAINER Fieldwork

RUN apk add --repository https://nl.alpinelinux.org/alpine/edge/testing flow
RUN apk add --update git && \
    rm -rf /tmp/* /var/cache/apk/*

RUN npm install -g npm@latest \
    npm install -g @feathersjs/cli sequelize sequelize-cli

CMD ["sh"]
