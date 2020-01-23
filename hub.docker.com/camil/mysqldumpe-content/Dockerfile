FROM node:alpine

RUN apk update
RUN apk add mysql-client

WORKDIR /home/node
USER node

COPY package*.json ./
RUN npm install

COPY . .

ENTRYPOINT [ "node", "index.js" ]