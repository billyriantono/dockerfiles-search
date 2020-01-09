FROM keymetrics/pm2:latest-alpine
RUN apk update && apk add ca-certificates && rm -rf /var/cache/apk/*
ENV NPM_CONFIG_LOGLEVEL warn
ENV NODE_ENV=production

RUN mkdir -p /base

COPY ./ /base