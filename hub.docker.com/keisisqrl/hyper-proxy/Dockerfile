FROM alpine:3.6

WORKDIR /app

RUN apk add --no-cache caddy nodejs-npm

ADD . /app

RUN npm install && touch Caddyfile

CMD npm start
