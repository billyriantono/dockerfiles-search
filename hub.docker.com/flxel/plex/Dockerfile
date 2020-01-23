FROM flxel/base:latest
MAINTAINER elseym <elseym@me.com>

# configure
EXPOSE 32400
ENV PMS_VERSION 1.13.6.5339-115f087d6
ENV HOME /config/plexmediaserver
ENV FLXEL_SERVICE_CMD /usr/sbin/start_pms

# install software
RUN curl -Lo /tmp/plex.deb https://downloads.plex.tv/plex-media-server/${PMS_VERSION}/plexmediaserver_${PMS_VERSION}_amd64.deb && \
    mv /sbin/udevadm /sbin/udevadm.bak; touch /sbin/udevadm; chmod +x /sbin/udevadm && \
    dpkg -i /tmp/plex.deb && \
    mv /sbin/udevadm.bak /sbin/udevadm && \
    rm /tmp/plex.deb && \
    apt-get -yf install
