FROM alpine:3.2

MAINTAINER Peter Sorowka <sorowka@cybus.io>

EXPOSE 80 443

RUN apk add --update bash nginx && rm -rf /var/cache/apk/*

CMD ["nginx", "-g", "daemon off;"]
