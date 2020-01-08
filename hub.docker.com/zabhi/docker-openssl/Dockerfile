FROM alpine:3.6

MAINTAINER Abhishek Kumar (https://github.com/zabhi)

RUN apk add --no-cache openssl && \
  rm -rf /var/cache/apk/*

ENTRYPOINT ["openssl"]
