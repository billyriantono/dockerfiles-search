FROM dockeredcom/debian-stretch-gpg:latest

MAINTAINER Yves Vindevogel (yves.vindevogel@dockered.com)

ENV SHELL=/bin/bash
ENV ISSO_HOST="http://localhost:8820/"
ENV ISSO_LISTEN="http://0.0.0.0:8080/"

ARG DEBIAN_FRONTEND=noninteractive

COPY ./isso.conf /etc/isso/isso.conf
COPY ./start.sh /srv/script/start.sh

RUN set -x && \ 
    chmod +x /srv/script/start.sh && \ 
    mkdir -p /srv/db && \ 
    apt-get update --yes && \ 
    apt-get upgrade --yes && \ 
    apt-get install dialog python-pip sqlite3 build-essential --yes && \ 
    pip install isso && \ 
    echo "[general]"                        >   /etc/isso/isso.conf && \ 
    echo "dbpath = /srv/db/comments.db"     >>  /etc/isso/isso.conf && \ 
    echo "host = $ISSO_HOST"                >>  /etc/isso/isso.conf && \ 
    echo "log-file = /var/log/isso.log"     >>  /etc/isso/isso.conf && \ 
    echo ""                                 >>  /etc/isso/isso.conf && \ 
    echo "[server]"                         >>  /etc/isso/isso.conf && \ 
    echo "listen = $ISSO_LISTEN"            >>  /etc/isso/isso.conf && \ 
    apt-get autoremove --yes && \ 
    apt-get clean && \ 
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

ENTRYPOINT ["/srv/script/start.sh"]
