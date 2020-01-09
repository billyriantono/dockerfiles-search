FROM hypriot/rpi-alpine-scratch:v3.2
MAINTAINER Vitor Silva Lima <vitor.lima2@fatec.sp.gov.br>

#Upgrades the current image and install Mosquitto on it
RUN echo "http://dl-4.alpinelinux.org/alpine/latest-stable/main/"      | tee /etc/apk/repositories    \
 && echo "http://dl-4.alpinelinux.org/alpine/latest-stable/community/" | tee -a /etc/apk/repositories \
 && apk -U --no-progress upgrade && rm -f /var/cache/apk/APKINDEX.* \
 && apk --no-cache --no-progress add mosquitto bash

#Create the directories which will be used to store Mosquitto's data
RUN mkdir -p /mqtt/config /mqtt/data /mqtt/log
COPY config /mqtt/config
COPY ws_client /mqtt/client
RUN chown -R mosquitto:mosquitto /mqtt
USER mosquitto

VOLUME ["/mqtt/data","/mqtt/log"]
#the ports which will be exposed
#1883 = mqtt
#9001 = websocket
EXPOSE 1883 9001

#starts Mosquitto
CMD ["/usr/sbin/mosquitto", "-c", "/mqtt/config/mosquitto.conf"]
