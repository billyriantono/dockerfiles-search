FROM node:10-alpine

WORKDIR /usr/src/app

COPY package*.json ./

RUN npm install

COPY lib/ lib/
COPY public/ public/
COPY webapp.js .babelrc ./

EXPOSE 3000
CMD [ "node", "webapp.js" ]