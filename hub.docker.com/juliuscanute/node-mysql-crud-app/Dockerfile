FROM node:alpine
MAINTAINER juliuscanute@touchcapture.net
RUN apk update && apk add --virtual build-deps npm git openssh && mkdir /usr/share/website
WORKDIR /usr/share/website
RUN git clone https://github.com/juliuscanute/node-mysql-crud-app.git && npm install node-mysql-crud-app \
    && rm -rf node-mysql-crud-app/.git && apk --purge -v del build-deps && rm /var/cache/apk/* \
    && rm -rf node-mysql-crud-app/deployment/* && mv node-mysql-crud-app/* . && mkdir -p public/assets/img/
EXPOSE 2000/tcp
ENTRYPOINT ["node","app.js"]
