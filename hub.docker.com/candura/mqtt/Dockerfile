#########################################
# MQTT broker: Mosquitto
#########################################

FROM alpine:latest

MAINTAINER iCandura <https://github.com/icandura>

# Install packages
RUN apk add --update mosquitto mosquitto-clients

# Expose MQTT port and websockets port
EXPOSE 1883
EXPOSE 1884

RUN echo "port 1883" >> /etc/mosquitto/mosquitto.conf
RUN echo "listener 1884" >> /etc/mosquitto/mosquitto.conf
RUN echo "protocol websockets" >> /etc/mosquitto/mosquitto.conf
RUN echo "allow_anonymous false" >> /etc/mosquitto/mosquitto.conf

ENTRYPOINT ["mosquitto"]
