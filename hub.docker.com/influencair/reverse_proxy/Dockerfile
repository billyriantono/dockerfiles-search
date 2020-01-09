FROM node:13-alpine AS release

WORKDIR /server
COPY package*.json ./

# install production dependencies
RUN npm i --only=prod

RUN apk add --no-cache tini
ENTRYPOINT ["/sbin/tini", "--"]

WORKDIR /server
COPY greenlock.json ./
COPY src/ ./
COPY public/ ./public/

CMD ["node", "index"]