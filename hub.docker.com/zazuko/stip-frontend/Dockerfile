FROM node:8

RUN mkdir -p /usr/src/app
WORKDIR /usr/src/app

COPY package.json yarn.lock /usr/src/app/
RUN yarn install --pure-lockfile && yarn cache clean

COPY . /usr/src/app
RUN yarn build

ENV NODE_ENV production

RUN yarn global add pm2
CMD pm2-docker start server.js

EXPOSE 3000
