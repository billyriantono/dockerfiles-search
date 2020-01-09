FROM node:12.4.0-alpine

RUN mkdir /webapp
WORKDIR /webapp

RUN npm i -g yarn

COPY package.json /webapp/package.json
COPY yarn.lock /webapp/yarn.lock

RUN yarn install
