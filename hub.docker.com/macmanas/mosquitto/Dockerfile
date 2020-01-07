FROM lsiobase/alpine
MAINTAINER MacManas <diegomanas.dev@gmail.com>

# Set version label
LABEL Description="Eclipse Mosquitto MQTT Broker"

# Copy local files
COPY root/ /

RUN apk --no-cache add mosquitto=1.4.12-r0 && \
    mkdir -p /defaults && \
    mkdir -p /config /data /log && \
    cp /etc/mosquitto/mosquitto.conf /defaults/mosquitto.conf

# Ports and volumes
EXPOSE 1883 9001
VOLUME /config /log /data