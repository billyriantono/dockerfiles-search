FROM alpine:3.3

ENV VARNISH_MEMORY 100M

RUN apk add --no-cache varnish

COPY default.vcl /etc/varnish/default.vcl
COPY varnish-foreground /usr/local/bin/

EXPOSE 80

CMD ["varnish-foreground"]