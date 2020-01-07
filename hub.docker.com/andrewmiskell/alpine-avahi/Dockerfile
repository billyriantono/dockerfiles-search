FROM arm32v6/alpine:latest

LABEL MAINTAINER="Andrew Miskell <andrewmiskell@mac.com>" \
    Description="Lightweight Avahi docker container, based on Alpine Linux."

# copy qemu-arm-static to /usr/bin to allow automated builds for arm on docker-hub
COPY dockerfile/armhf/qemu-arm-static /usr/bin

# upgrade base system and install samba and supervisord
RUN apk --no-cache upgrade && apk --no-cache add avahi supervisor

# disable dbus support in avahi
RUN sed -i 's/#enable-dbus=yes/enable-dbus=no/g' /etc/avahi/avahi-daemon.conf

# copy supervisord configuration file into place
COPY supervisord.conf /etc/supervisord.conf

# volume mappings
VOLUME /etc/avahi/services

# exposes avahi's default port (5353/udp)
EXPOSE 5353/udp

ENTRYPOINT ["supervisord", "-c", "/etc/supervisord.conf"]
