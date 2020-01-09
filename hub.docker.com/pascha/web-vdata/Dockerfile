FROM busybox:buildroot-2014.02

MAINTAINER Pascha Butretell <admin@pascha.domains>

RUN    adduser -u 3342 -D pascha \
    && mkdir -p /volumes/web-data \
    && chown pascha:pascha /volumes/web-data \
    && chmod 770 /volumes/web-data

VOLUME ["/volumes/web-data"]