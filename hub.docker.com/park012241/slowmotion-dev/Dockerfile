FROM node:12-alpine
MAINTAINER Joosung Park <admin@slowmotion.dev>

add . /app
WORKDIR /app

RUN yarn && yarn build

CMD yarn serve
EXPOSE 8080
