FROM alpine:latest

MAINTAINER Adam Copley <adam.copley@arola.co.uk>

ARG VERSION=1.14.2-r0

RUN apk update && \
  apk add \
  nginx=${VERSION}

RUN mkdir -p /data/nginx/cache
RUN mkdir -p /run/nginx

COPY nginx.conf /etc/nginx/nginx.conf
RUN chmod 644 /etc/nginx/nginx.conf

CMD ["nginx", "-g", "daemon off;"]
