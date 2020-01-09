############################################################
# Dockerfile zum erstellen eines Dockercontainers für
# homegear
############################################################

############################################################
# Argument Variables from YAML File
############################################################

FROM derbrummbaer/rpi-raspbian:jessie

# File Author / Maintainer
MAINTAINER Sven Berger

############################################################
############################################################
# USE CROSS-BUILD for Raspberry PI Images
############################################################
############################################################

RUN [ "cross-build-start" ]

############################################################
# don't ask for stupid things
############################################################

ENV DEBIAN_FRONTEND noninteractive
RUN echo APT::Install-Recommends "0"; >> /etc/apt/apt.conf
RUN echo APT::Install-Suggests "0"; >> /etc/apt/apt.conf

############################################################
# Environment Variables
############################################################

############################################################
# User Ändern
############################################################

############################################################
# Upgrade Software: Installed
############################################################

# Repository für Pilight
RUN apt-get update && \
	apt-get install apt-transport-https wget ca-certificates apt-utils gnupg -qy

############################################################
# Install Software: Homegear
############################################################


RUN echo 'deb https://apt.homegear.eu/Raspbian/ jessie/' >> /etc/apt/sources.list.d/homegear.list && \
    wget -O - https://apt.homegear.eu/Release.key | apt-key add -
    
RUN apt-get update && \
    apt-get dist-upgrade -qy && \
    apt-get install -qy \
    libavahi-client3 \
    libavahi-client-dev \
    insserv
#   libzip4 \
RUN apt-get update && \
    apt-get dist-upgrade -qy && \
    apt-get install -qy \
	homegear \
    homegear-management \
    homegear-webssh \
    homegear-adminui \
    homegear-nodes-core \
    homegear-nodes-extra \
    homegear-homematicbidcos \
    homegear-homematicwired \
    homegear-max \
    homegear-kodi \
    homegear-intertechno \
    homegear-knx
    
    # homegear-influxdb \
    # homegear-insteon \
    # homegear-philipshue \
    # homegear-sonos \
    # homegear-ipcam \
    # homegear-beckhoff \
    # homegear-enocean \
    # homegear-mbus \
    # homegear-ccu2 \
    # homegear-zwave \




############################################################
# Remove Apt Data
############################################################

RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

############################################################
# Copy External Data
############################################################

RUN rm -f /etc/homegear/dh1024.pem; \
    rm -f /etc/homegear/homegear.crt; \
    rm -f /etc/homegear/homegear.key; \
    cp -R /etc/homegear /etc/homegear.config; \
    cp -R /var/lib/homegear /var/lib/homegear.data

############################################################
# Copy Start Scripts
############################################################

COPY scripte/run.sh /usr/local/bin/run.sh
RUN chmod +x /usr/local/bin/run.sh

############################################################
# Folders needed
############################################################

VOLUME ["/etc/homegear", "/var/lib/homegear", "/var/log/homegear"]

############################################################
# Ports needed
############################################################

EXPOSE 2001 2002 2003

############################################################
############################################################
# USE CROSS-BUILD for Raspberry PI Images
############################################################
############################################################

RUN [ "cross-build-end" ]

############################################################
# Container Start
############################################################

ENTRYPOINT ["/bin/bash", "-c", "/usr/local/bin/run.sh"]
