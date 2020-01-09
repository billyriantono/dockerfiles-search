FROM node:10.11-stretch

# Set environment variables
ENV DEBIAN_FRONTEND noninteractive
ENV TERM xterm

RUN apt-get update; \
    apt-get install -y apt-utils apt-transport-https; \
    apt-get install -y curl wget; \
    apt-get install -y libnss-mdns avahi-discover libavahi-compat-libdnssd-dev libkrb5-dev; \
    apt-get install -y ffmpeg; \
    apt-get install -y nano vim

RUN npm install -g homebridge --unsafe-perm

# MISC settings
COPY avahi-daemon.conf /etc/avahi/avahi-daemon.conf

USER root
RUN mkdir -p /var/run/dbus

ADD run.sh /root/run.sh
RUN chmod a+x /root/run.sh

# Run container
EXPOSE 5353 51826
VOLUME [ "/root/.homebridge" ]
CMD ["/root/run.sh"]
