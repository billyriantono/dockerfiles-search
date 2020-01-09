FROM alpine:3.5
MAINTAINER Tim Haak <tim@haak.co>

ENV LANG='en_US.UTF-8' \
    LANGUAGE='en_US.UTF-8' \
    TERM='xterm'

RUN apk -U add ca-certificates git py2-openssl py-libxml2 py2-lxml && \
    git clone --depth 1 https://github.com/RuudBurger/CouchPotatoServer.git && \
    rm -rf /var/cache/apk/*

VOLUME ["/config", "/data"]

COPY start.sh /start.sh

EXPOSE 5050

CMD ["/start.sh"]
