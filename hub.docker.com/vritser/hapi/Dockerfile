FROM node:slim

RUN mkdir -p /usr/src/app
WORKDIR /usr/src/app

COPY app/package.json /usr/src/app
RUN yarn

COPY app /usr/src/app

EXPOSE 3000

CMD yarn start
