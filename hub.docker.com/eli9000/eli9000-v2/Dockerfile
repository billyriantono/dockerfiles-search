FROM node:latest

LABEL name="eli9000-v2"
LABEL version="2.0.0"
LABEL maintainer="Eli Johnson <eli9000@gmail.com>"

WORKDIR /usr/src/app

ARG NODE_ENV=production

ENV NPM_CONFIG_LOGLEVEL warn

COPY package.json package-lock.json ./

RUN npm install

RUN npm build

COPY . .

EXPOSE 9000

CMD [ "node", "server/index.js" ]

