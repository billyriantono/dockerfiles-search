FROM node:12-alpine as base

RUN yarn global add express-generator

WORKDIR /app

CMD yarn install && yarn start

FROM base as build

COPY src .

RUN yarn install --production

CMD yarn start
