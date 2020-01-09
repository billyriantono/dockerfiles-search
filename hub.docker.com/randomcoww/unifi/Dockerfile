FROM openjdk:8-jre-alpine

ENV UNIFI_VERSION 5.12.35
ENV UNIFI_PATH /opt/UniFi

RUN set -x \
  \
  && wget -O /tmp/unifi.zip http://dl.ubnt.com/unifi/$UNIFI_VERSION/UniFi.unix.zip \
  && mkdir -p /opt \
  && unzip /tmp/unifi.zip -d /opt \
  && rm /tmp/unifi.zip \
  \
  && mkdir -p $UNIFI_PATH/logs \
  && ln -fs /dev/stdout $UNIFI_PATH/logs/server.log \
  && ln -fs /dev/null $UNIFI_PATH/logs/mongod.log \
  \
  && apk add --no-cache \
    mongodb \
    gcompat \
  && rm \
    /usr/bin/mongo \
    /usr/bin/mongos

COPY docker-entrypoint.sh /
COPY docker-stop.sh /

WORKDIR $UNIFI_PATH
ENTRYPOINT ["/docker-entrypoint.sh"]
