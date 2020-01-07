FROM alpine:3.8

LABEL maintainer "Ben Roberts <ben@headsnet.com>"

RUN apk --no-cache add apache2 apache2-utils apache2-proxy

RUN mkdir -p /run/apache2/

COPY httpd.conf /etc/apache2/httpd.conf

EXPOSE 80

COPY scripts/entrypoint.sh /
RUN chmod +x /entrypoint.sh

ENTRYPOINT ["/entrypoint.sh"]
