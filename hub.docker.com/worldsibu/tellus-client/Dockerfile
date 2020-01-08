FROM node:carbon

RUN apt-get update
RUN apt-get upgrade -y
RUN apt-get -y install autoconf automake libtool nasm make pkg-config git apt-utils

WORKDIR /usr/src/app

# Handle NPM installation here, so if we don't change any dependency
# Docker doesn't have to rebuild and install again
COPY package*.json ./
COPY .npmrc ./
RUN npm install
RUN npm rebuild

COPY api ./api
COPY config ./config
COPY test-ui ./test-ui

COPY scripts ./scripts
COPY chaincode-views ./chaincode-views

COPY app.js ./
COPY .env ./
COPY pm2.config.json ./

EXPOSE 10010
EXPOSE 9222

CMD [ "npm", "start" ]

RUN exit 0
