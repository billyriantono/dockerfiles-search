FROM alpine:3.2
MAINTAINER Denys Chekirda aka Rocklviv <denis.chekirda@leoengine.org>

RUN apk update && apk add nginx && rm -rf /var/cache/apk
COPY configs/ /etc/nginx
EXPOSE 80 443
CMD ["nginx"]
