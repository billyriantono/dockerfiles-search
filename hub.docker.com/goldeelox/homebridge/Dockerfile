FROM debian:jessie

RUN apt-get update
RUN apt-get install -y curl build-essential avahi-daemon avahi-discover libnss-mdns libavahi-compat-libdnssd-dev
RUN curl -sL https://deb.nodesource.com/setup_6.x | bash -
RUN apt-get install -y nodejs
RUN npm install -g homebridge
RUN npm install -g homebridge-wemo
RUN npm install -g homebridge-wol

EXPOSE 40745 5353

RUN mkdir -p /var/run/dbus
RUN mkdir -p /opt/homebridge

COPY config/config.json /opt/homebridge
COPY config/run.sh /opt/run.sh
RUN chmod +x /opt/run.sh

VOLUME /opt/homebridge

CMD ["/opt/run.sh"]
