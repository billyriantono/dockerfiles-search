FROM explee/nginx:latest

MAINTAINER Morgan Giraud <morgan@explee.com>

ENV EXPLEE_VARNISH_HOST varnish
ENV EXPLEE_VARNISH_PORT 6081

RUN rm /etc/nginx/conf.d/*
COPY .htpasswd /etc/nginx/.htpasswd
COPY ping.conf /etc/nginx/conf.d/ping.conf
COPY varnish.template /etc/nginx/conf.d/varnish.template

EXPOSE 80
EXPOSE 8001

COPY docker-entrypoint.sh /entrypoint.sh
RUN chown explee:explee /entrypoint.sh
ENTRYPOINT ["/entrypoint.sh"]