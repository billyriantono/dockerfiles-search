FROM alpine:3.5
MAINTAINER WPLib Team <team@wplib.org>

RUN apk add --no-cache bash \
  apache2=2.4.25-r0 \
  apache2-proxy=2.4.25-r0 \
  apache2-ssl=2.4.25-r0 \
  && mkdir -p /run/apache2 \
  && ln -sf /dev/stdout /var/log/apache2/access.log \
  && ln -sf /dev/stderr /var/log/apache2/error.log

COPY files /

EXPOSE 80 443

CMD ["/usr/sbin/httpd", "-DFOREGROUND"]