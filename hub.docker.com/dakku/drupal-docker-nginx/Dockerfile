FROM nginx:alpine

ENV APP_ROOT="/var/www/html"

RUN apk add --update --no-cache \
    bash \
    nano \
    wget

WORKDIR $APP_ROOT