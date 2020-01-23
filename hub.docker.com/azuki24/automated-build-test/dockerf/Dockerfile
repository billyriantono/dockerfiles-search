FROM alpine

RUN apk add --update aria2 && rm -rf /var/cache/apk/*

ADD https://github.com/kelseyhightower/confd/releases/download/v0.16.0/confd-0.16.0-linux-amd64 /usr/bin/confd

RUN chmod +x /usr/bin/confd

COPY ./confd /etc/confd

VOLUME /downloads

# aria2 RPC port, map as-is or reconfigure webui

# webui static content web server, map wherever is convenient
EXPOSE 6800/tcp

#CMD aria2c --conf-path=/etc/aria2.conf
CMD confd -onetime -backend env && aria2c --conf-path=/etc/aria2.conf
