FROM alpine:latest
LABEL org.freenas.interactive="true" \
      org.freenas.command="/bin/sh" \
      org.freenas.version="2" \
      org.freenas.upgradeable="false" 
RUN apk update && apk upgrade && apk add openssh rdiff-backup bash
