FROM busybox:buildroot-2014.02

MAINTAINER Pascha Butretell <admin@pascha.domains>

RUN    adduser -u 3342 -D pascha \
    && mkdir -p /volumes/dbdweb-data \
    && chown pascha:pascha /volumes/dbdweb-data \
    && chmod 770 /volumes/dbdweb-data

VOLUME ["/volumes/dbdweb-data"]