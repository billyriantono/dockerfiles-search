FROM gkrio/node:latest

RUN apk update && apk add --no-cache supervisor \
    && mkdir -p /etc/supervisor/conf.d/ \
    && mkdir -p /var/log/supervisor/

COPY supervisord.conf /etc/supervisor/supervisord.conf

VOLUME ["/etc/supervisor/conf.d"]

CMD ["/usr/bin/supervisord","-n","-c","/etc/supervisor/supervisord.conf"]
