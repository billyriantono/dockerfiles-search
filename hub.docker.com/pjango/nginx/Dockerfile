FROM nginx

MAINTAINER Pjango <info@pjango.com>

# Add files
COPY resources/confd/conf.d /etc/confd/conf.d

COPY resources/confd/templates /etc/confd/templates

COPY docker-entrypoint.sh /usr/local/bin/

EXPOSE 80 443

ENTRYPOINT ["docker-entrypoint.sh"]