FROM node:8-alpine

WORKDIR /usr/src/yapi/vendors

COPY config.json /usr/src/yapi/config.json

COPY vendors/ /usr/src/yapi/vendors/

RUN npm install --production --registry https://registry.npm.taobao.org

CMD node server/app.js

