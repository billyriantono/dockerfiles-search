FROM node:alpine

ENV NODE_PORT=8880

RUN apk add --no-cache git

WORKDIR /usr/src/app

COPY package*.json yarn.lock ./
RUN yarn --no-cache --frozen-lockfile


COPY . .
RUN yarn run build

EXPOSE $NODE_PORT

ENV NODE_ENV=production
CMD ["node", "dist/server.js"]