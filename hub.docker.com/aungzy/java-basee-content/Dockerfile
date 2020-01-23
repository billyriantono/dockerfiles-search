FROM alpine:3.8

MAINTAINER "Audite Marlow <https://github.com/AuditeMarlow>"

ENV USERNAME admin
ENV PASSWORD password

COPY src/ .

RUN apk --no-cache --update add transmission-daemon shadow \
    && groupmod -g 1000 transmission \
    && usermod -u 1000 transmission \
    && mkdir -p \
        /transmission/downloads \
        /transmission/incomplete \
        /etc/transmission-daemon \
        /var/lib/transmission-daemon \
    && chown -R transmission:transmission /transmission \
    && chown -R transmission:transmission /etc/transmission-daemon \
    && chown -R transmission:transmission /var/lib/transmission-daemon

EXPOSE 9091 51413/tcp 51413/udp

USER transmission

CMD ["/start-transmission.sh"]
