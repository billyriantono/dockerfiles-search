FROM alpine:3.4
MAINTAINER Eduardo Ramos <eduardorfreitas93@gmail.com>

RUN apk --no-cache --update add python py-pip docker \ 
    && pip install supervisor \ 
    && rm -rf /var/cache/apk/*

ADD supervisord.conf /etc/

ENTRYPOINT ["supervisord", "--nodaemon", "--configuration", "/etc/supervisord.conf"]
