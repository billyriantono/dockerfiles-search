FROM       alpine
MAINTAINER Viacheslav Kalashnikov <xemuliam@gmail.com>
ARG        RETHINKDB_VERSION=2.3.5-r7
RUN        apk update && apk add --upgrade bash jq rethinkdb=$RETHINKDB_VERSION && \
           rm -rf /var/cache/apk/*
EXPOSE     28015 29015 8080
VOLUME     /data
WORKDIR    /data
CMD       rethinkdb --bind all
