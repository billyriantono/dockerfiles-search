FROM node:11-alpine
RUN apk update && apk add --no-cache make python git && npm install -g yapi-cli --registry https://registry.npm.taobao.org
WORKDIR /my-yapi
CMD node vendors/server/app.js