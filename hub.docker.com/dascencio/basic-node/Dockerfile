FROM node:12-alpine AS builder

WORKDIR /tmp/app

COPY package*.json ./

RUN npm install

FROM node:12-alpine

WORKDIR /usr/src/app

COPY --from=builder --chown=node:node /tmp/app/node_modules ./node_modules
COPY --chown=node:node . ./

EXPOSE 3000

CMD [ "node", "server.js" ]

USER node
