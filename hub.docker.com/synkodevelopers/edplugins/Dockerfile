FROM node:9-alpine

COPY package.json yarn.lock ./

RUN yarn install

COPY . .

ENV webhook=true
ENV webhook_reply=false

EXPOSE 3000

CMD npm start
