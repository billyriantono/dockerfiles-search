FROM cloudcube/alinode

MAINTAINER zhaohaibin@outlook.com

USER root

ADD . /root/webapp

RUN \
    apt-get update && \
    apt-get install imagemagick --fix-missing -y && \
    rm -rf /var/lib/apt/lits/*

RUN mv /root/webapp/config.default.js /root/webapp/config.js

WORKDIR /webapp

VOLUME /webapp

COPY docker-entrypoint.sh /

ADD supervisor_linqmind.conf /etc/supervisor/conf.d/linqmind.conf

ENTRYPOINT ["/docker-entrypoint.sh"]


