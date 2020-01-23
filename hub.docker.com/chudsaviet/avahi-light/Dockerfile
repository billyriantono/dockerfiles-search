FROM alpine:3.9

RUN apk add --no-cache avahi tini \
    && rm -r /etc/avahi/services/* \
    && sed -i -- 's/#enable-dbus=yes/enable-dbus=no/g' /etc/avahi/avahi-daemon.conf

ENTRYPOINT [ "/sbin/tini", "avahi-daemon" ]