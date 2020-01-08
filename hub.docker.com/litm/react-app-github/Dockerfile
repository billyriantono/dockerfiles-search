FROM node:10-alpine

WORKDIR /urs/app

COPY package.json .

RUN npm install

COPY src src

COPY public public

CMD ["npm","start"]

