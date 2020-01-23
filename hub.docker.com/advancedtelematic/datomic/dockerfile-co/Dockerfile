FROM alpine:3.5
MAINTAINER  Adrien MILLOT <adrien.millot@gmail.com>

ENV VARNISH_MEMORY 100M

RUN apk add --no-cache varnish

COPY start.sh /usr/local/bin/docker-varnish-start

RUN chmod +x /usr/local/bin/docker-varnish-start

CMD ["docker-varnish-start"]