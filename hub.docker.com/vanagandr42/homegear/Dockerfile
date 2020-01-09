FROM lsiobase/ubuntu:108

# Package version
ARG HOMEGEAR_VER="0.7.19"

# Environment settings
ARG DEBIAN_FRONTEND="noninteractive"

# Install dependencies
RUN apt-get update \
 && apt-get install -y wget apt-transport-https --no-install-recommends \
 && wget -P /tmp https://homegear.eu/packages/Release.key \
 && apt-key add /tmp/Release.key \
 && echo 'deb https://homegear.eu/packages/Ubuntu/ xenial/' >> /etc/apt/sources.list.d/homegear.list \
 && apt-get update \
 && apt-get install -y homegear homegear-nodes-core homegear-homematicbidcos --no-install-recommends \
 && mv /etc/homegear /defaults/config \
 && mv /usr/share/homegear /defaults/files \
 && mv /var/lib/homegear /defaults/data \
 && rmdir /var/log/homegear \
 && rmdir /var/run/homegear \
 
# Cleanup
 && rm -rf /var/lib/apt/lists/* \
           /tmp/*

# Declare volumes
VOLUME ["/config", \
        "/app"]

# Add local files
COPY rootfs/ /

# Expose port of the webservice
EXPOSE 2001/tcp \
       2002/tcp \
       2003/tcp
