FROM phusion/baseimage:latest
MAINTAINER gino <ginorh@gmail.com>
ENV DEBIAN_FRONTEND noninteractive

# Set correct environment variables
ENV HOME /root

# Fix a Debianism of the nobody's uid being 65534
RUN usermod -u 99 nobody && \
usermod -g 100 nobody && \
apt-get update -q && \

# Upgrade
apt-get dist-upgrade -y && \

# Install Dependencies
apt-get install -qy apt-utils unrar-free git-core openssl libssl-dev sudo \
python2.7 ca-certificates wget unzip vim-nox && \

mkdir /opt/sickrage && \
chown -R nobody:users /opt/sickrage && \
sudo -u nobody git clone https://github.com/SickRage/SickRage.git /opt/sickrage && \

# clean up
apt-get clean && \
rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* \
/usr/share/man /usr/share/info \
/usr/share/lintian /var/cache/man
#(( find /usr/share/doc -depth -type f ! -name copyright|xargs rm || true )) && \
#(( find /usr/share/doc -empty|xargs rmdir || true ))

ADD ./startsickrage.sh /startsickrage.sh
RUN chmod u+x  /startsickrage.sh

EXPOSE 8081

# SickRage Configuration
VOLUME /config

# Downloads directory
VOLUME /downloads

# TV directory
VOLUME /media/TVSeries

RUN /startsickrage.sh
