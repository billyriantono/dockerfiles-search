FROM project42/s6-alpine:latest
MAINTAINER Jordan Clark jordan.clark@esu10.org

RUN apk add --no-cache php5-fpm

COPY container-files /

EXPOSE 9000

ENTRYPOINT ["/init"]
