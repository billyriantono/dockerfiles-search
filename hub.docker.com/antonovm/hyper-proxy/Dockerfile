FROM alpine:edge

WORKDIR /app

LABEL caddy_version="0.10.4" architecture="amd64"

ARG plugins=http.git,tls.dns.cloudflare

RUN apk add --no-cache git tar curl nodejs nodejs-npm && npm install npm@latest -g

RUN curl --silent --show-error --fail --location \
      --header "Accept: application/tar+gzip, application/x-gzip, application/octet-stream" -o - \
      "https://caddyserver.com/download/linux/amd64?plugins=${plugins}" \
    | tar --no-same-owner -C /usr/bin/ -xz caddy \
 && chmod 0755 /usr/bin/caddy \
 && /usr/bin/caddy -version

ADD . /app

RUN npm install && touch Caddyfile

RUN npm i -g pm2

CMD pm2-docker start npm -- start
