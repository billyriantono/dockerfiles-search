FROM debian:stretch-slim

LABEL maintainer "Espen Lorentzen <esplor@gmail.com>"

ENV EXTRA_PACKAGES less nano htop
ENV LANG C.UTF-8

RUN ln -sf /usr/share/zoneinfo/Europe/Oslo /etc/localtime \
    && echo "\
deb http://deb.debian.org/debian/           stretch         main contrib non-free\n\
deb http://deb.debian.org/debian/           stretch-updates main contrib non-free\n\
deb http://deb.debian.org/debian-security/  stretch/updates main contrib non-free\
" > /etc/apt/sources.list \
    && apt-get update \
    && apt-get --auto-remove -y dist-upgrade \
    && apt-get install --no-install-recommends --auto-remove -y $EXTRA_PACKAGES \
    && rm -rf /var/lib/apt/lists/*

CMD [ "/usr/bin/env", "sh" ]
