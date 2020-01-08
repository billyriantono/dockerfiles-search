FROM debian:jessie
MAINTAINER Wolfram Webers <wolfram.webers@gmail.com>

ENV DEBIAN_FRONTEND noninteractive
ENV LANG en_US.UTF-8
ENV LC_ALL C.UTF-8
ENV LANGUAGE en_US.UTF-8

RUN apt-get -q update && \
    apt-get -qy --force-yes dist-upgrade && \
    apt-get install -qy dbus nfs-common

RUN apt-get install -qy --force-yes curl && \
    echo "deb http://shell.ninthgate.se/packages/debian wheezy main" > /etc/apt/sources.list.d/plexmediaserver.list && \
    curl http://shell.ninthgate.se/packages/shell-ninthgate-se-keyring.key | apt-key add - && \
    apt-get -q update && \
    apt-get -qy --force-yes dist-upgrade && \
    apt-get install -qy --force-yes supervisor ca-certificates procps && \
    apt-get install -qy --force-yes plexmediaserver && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* && \
    rm -rf /tmp/*

VOLUME /config
VOLUME /data

COPY ./plex.sh /usr/bin/
RUN chmod u+x /usr/bin/plex.sh

ADD ./supervisord.conf /etc/supervisor/conf.d/supervisord.conf

EXPOSE 32400

ENTRYPOINT ["plex.sh"]
