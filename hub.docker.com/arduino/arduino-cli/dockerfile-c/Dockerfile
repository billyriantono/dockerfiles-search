FROM alpine
MAINTAINER Adam Karim <adam@akarsoft.com>

RUN apk add --no-cache -q avahi tini && \
    sed -i'' 's/^#enable-dbus=yes/enable-dbus=no/' /etc/avahi/avahi-daemon.conf

COPY afpd.service /etc/avahi/services/afpd.service
COPY entrypoint.sh /entrypoint.sh

CMD /entrypoint.sh
