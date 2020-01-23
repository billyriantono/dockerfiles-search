FROM debian:wheezy

MAINTAINER “Dylan Lindgren” <dylan.lindgren@gmail.com>

WORKDIR /var/lib

# Install SickBeard & it's prerequisites
RUN apt-get update -y && \
    apt-get install -y \
    git \
    python2.7 \
    python-cheetah && \
    rm -rf /var/lib/apt/lists/* && \
    git clone git://github.com/midgetspy/Sick-Beard.git /var/lib/SickBeard

# Create SickBeard user and set permissions
RUN adduser -c "SickBeard User" sickbeard && \
    mkdir -p /data/sickbeard && \
    chown -R sickbeard:sickbeard /var/lib/SickBeard /data/sickbeard
VOLUME ["/data/sickbeard"]
VOLUME ["/data/nzb"]
VOLUME ["/data/tvshows"]
VOLUME ["/data/sabnzbd-dl"]
VOLUME ["/data/transmission-dl"]

EXPOSE 8081

USER sickbeard

ENTRYPOINT ["/usr/bin/python", "/var/lib/SickBeard/SickBeard.py", "--datadir=/data/sickbeard"]
