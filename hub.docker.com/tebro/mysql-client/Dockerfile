FROM alpine

MAINTAINER Richard Weber

RUN apk add --update mysql-client && rm -rf /var/cache/apk/*

ENTRYPOINT ["mysql"]

