FROM node:10-alpine

WORKDIR /usr/src/app

COPY package*.json ./
COPY index.js ./

RUN npm install

CMD [ "npm", "start" ]