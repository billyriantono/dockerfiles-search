FROM openjdk:8-alpine

LABEL maintainer="Yago Lima <yagotoledolima@gmail.com"

COPY hbase-0.98.8-hadoop2 /opt/hbase

WORKDIR /opt/hbase

VOLUME /var/hbase

ENTRYPOINT [ "/opt/hbase/bin/start-hbase.sh" ]
