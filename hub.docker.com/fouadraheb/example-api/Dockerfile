FROM node:latest

WORKDIR /usr/src/api

COPY . .

ENV NODE_ENV=production

RUN npm install

CMD ["node", "index.js"]
