FROM ubuntu:latest
ENV DEBIAN_FRONTEND noninteractive
MAINTAINER Serafeim Mellos <fim@mellos.io>

ARG SKYPE_URL=https://repo.skype.com/latest/skypeforlinux-64.deb

RUN apt-get update && apt-get install -y gdebi curl && \
    curl -L -o /tmp/skype.deb $SKYPE_URL && \
    gdebi -n /tmp/skype.deb && apt-get remove --purge -y gdebi curl && \
    rm /tmp/skype.deb && SUDO_FORCE_REMOVE=yes apt autoremove -y && \
    rm -rf /var/lib/apt/lists/*

ADD start_skype.sh /usr/local/bin/
CMD ["/usr/local/bin/start_skype.sh"]
