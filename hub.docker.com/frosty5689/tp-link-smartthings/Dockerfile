FROM node:8-alpine

LABEL maintainer frosty5689 <frosty5689@gmail.com>

RUN apk add --no-cache --update \
    ca-certificates \
    tzdata \
  && update-ca-certificates \
  && rm -rf /root/.cache

RUN apk add --no-cache --update --virtual build-dependencies wget unzip && \
    wget -O /tmp/smartthings-tplink-master.zip https://github.com/DaveGut/TP-Link-SmartThings/archive/master.zip && \
    ls -l /tmp && \
    mkdir -p /opt && \
    unzip /tmp/smartthings-tplink-master.zip -d /opt && \
    mv "/opt/TP-Link-SmartThings-master/NodeJS Files" /opt/smartthings-tplink && \
    cd /opt/smartthings-tplink && \
    rm -rf /tmp/smartthings-tplink-master.zip && \
    apk del build-dependencies

ADD run/* /opt/smartthings-tplink/

WORKDIR /opt/smartthings-tplink/

EXPOSE 8082/tcp

CMD ["/opt/smartthings-tplink/start.sh"]

