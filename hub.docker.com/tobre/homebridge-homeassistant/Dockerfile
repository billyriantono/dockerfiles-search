FROM node:4

RUN apt-get update
RUN apt-get install -y --no-install-recommends avahi-daemon avahi-discover libnss-mdns libavahi-compat-libdnssd-dev
RUN apt-get install -y --no-install-recommends curl wget git apt-transport-https python build-essential make g++ libavahi-compat-libdnssd-dev libkrb5-dev vim net-tools
RUN npm install -g --unsafe-perm homebridge
RUN npm install -g --unsafe-perm homebridge-homeassistant

RUN mkdir -p /var/run/dbus

EXPOSE 51826

ADD docker/entrypoint.sh /root/entrypoint.sh
RUN chmod +x /root/entrypoint.sh

ENTRYPOINT ["/root/entrypoint.sh"]
