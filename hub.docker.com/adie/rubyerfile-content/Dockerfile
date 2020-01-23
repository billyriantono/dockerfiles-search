# Set base os
FROM debian:jessie

# Maintainer of this project
MAINTAINER Adelin <eclipse.magick@gmail.com>

# ENV DEBIAN_FRONTEND noninteractive

# Install repos and packages 
RUN apt-get update && apt-get -y upgrade

# Install software and repos
RUN apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys B42317285E12C7CF
RUN echo "deb http://apt.tvheadend.org/unstable/ jessie main" > /etc/apt/sources.list.d/tvheadend.list

RUN apt-get update
RUN apt-get install -y apt-utils debconf-utils debhelper libhdhomerun1 libnfs4 hdhomerun-config xmltv-util dvb-apps

RUN echo "tvheadend tvheadend/admin_password password 1234" | debconf-set-selections
RUN echo "tvheadend tvheadend/admin_username string admin" | debconf-set-selections

RUN apt-get install -y tvheadend

# Clean up APT and temporary files 
RUN apt-get install -f && apt-get remove --purge -y
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN mkdir -p /home/hts/videos && chown -R hts:video /home/hts/videos

EXPOSE 9981 9982

# add a user to run as non root
# RUN adduser --disabled-password --gecos '' admin

# VOLUME /config /recordings /data
VOLUME /home/hts/videos

ENTRYPOINT ["/usr/bin/tvheadend"]
CMD ["-C","-u","hts","-g","hts"]

