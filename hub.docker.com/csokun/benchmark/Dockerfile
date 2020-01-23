FROM node:lts-alpine

RUN apk add --no-cache python

COPY package.json /app/package.json
WORKDIR /app
RUN npm i autocannon concurrently --save

RUN ln -s /app/node_modules/.bin/autocannon /usr/local/bin/autocannon
RUN ln -s /app/node_modules/.bin/concurrently /usr/local/bin/concurrently

CMD [ "sh" ]