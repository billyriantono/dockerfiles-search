FROM nerelohw/docker-alpine
MAINTAINER Hongshun Yang<wholerencom@gmail.com>

RUN apk add -U --no-cache nodejs nodejs-npm \
 && npm --quiet install npm@latest -g \
 && npm --quiet install apidoc -g \
 && rm -rf /var/cache/apk/*


