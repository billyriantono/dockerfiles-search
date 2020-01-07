FROM alpine:3.3

MAINTAINER Harry Danes <docker@hdanes.nl>

RUN apk update && \
  apk upgrade && \
  apk add nginx-lua && \
  rm -rf /var/cache/apk/*

COPY nginx.conf /etc/nginx/nginx.conf

EXPOSE 80

ENTRYPOINT ["nginx", "-g", "daemon off;"]
