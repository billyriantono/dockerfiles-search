
FROM node:10-alpine

WORKDIR /usr/app

COPY package.json .

RUN yarn install

COPY src src
COPY public public

CMD ["yarn", "start"]