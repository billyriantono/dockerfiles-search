FROM node:8-alpine

WORKDIR /usr/src/app

COPY package*.json .

RUN npm i

COPY . .

RUN echo '{ "content": "content.quakejs.com" }' > bin/web.json

CMD node bin/web.js --config ./web.json
