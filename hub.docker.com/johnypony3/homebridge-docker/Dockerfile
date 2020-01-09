FROM nodesource/jessie

##################################################
# Set environment variables                      #
##################################################

ENV DEBIAN_FRONTEND noninteractive
ENV TERM xterm

##################################################
# Install tools                                  #
##################################################

RUN apt-get update
RUN apt-get install -y apt-utils
RUN apt-get install -y apt-transport-https
RUN apt-get install -y locales
RUN apt-get install -y curl wget git python build-essential make g++ libavahi-compat-libdnssd-dev libkrb5-dev vim net-tools nano
RUN apt-get install -y avahi-daemon avahi-discover libnss-mdns libavahi-compat-libdnssd-dev
RUN alias ll='ls -alG'

##################################################
# Install homebridge                             #
##################################################

RUN npm install -g homebridge@0.4.20 --unsafe-perm

RUN npm install -g homebridge-homeassistant --unsafe-perm
RUN npm install -g homebridge-mqtt-contactsensor --unsafe-perm
RUN npm install -g homebridge-mqtt-humidity --unsafe-perm
RUN npm install -g homebridge-mqtt-sensor --unsafe-perm
RUN npm install -g homebridge-mqtt-temperature --unsafe-perm
RUN npm install -g homebridge-mqttlightbulb --unsafe-perm
RUN npm install -g homebridge-mqttswitch --unsafe-perm
RUN npm install -g homebridge-nest --unsafe-perm
RUN npm install -g homebridge-server --unsafe-perm
RUN npm install -g homebridge-smartthings --unsafe-perm

##################################################
# Start                                          #
##################################################

USER root
RUN mkdir -p /var/run/dbus

EXPOSE 5353 51826 8765
CMD ["/root/run.sh"]
