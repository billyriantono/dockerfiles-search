#name of container: xowa
#versison of container: 0.0.1
FROM quantumobject/docker-baseimage:18.04
MAINTAINER Thomas Balogh "tbalogh_cvg@yahoo.com"

ENV DEBIAN_FRONTEND=noninteractive HOME="/config" TERM=xterm LANG=en_US.UTF-8 LANGUAGE=en_US:en LC_ALL=en_US.UTF-8

# Update the container
RUN apt-get update && apt-get install -y -q openjdk-8-jre unzip bzip2 p7zip-full wget mc \
                    && apt-get clean \
                    && rm -rf /tmp/* /var/tmp/*  \
                    && rm -rf /var/lib/apt/lists/*

COPY pre-conf.sh /sbin/pre-conf
RUN chmod +x /sbin/pre-conf; sync \
    && /bin/bash -c /sbin/pre-conf \
    && rm /sbin/pre-conf

RUN mkdir -p /etc/my_init.d
COPY startup.sh /etc/my_init.d/startup.sh
RUN chmod +x /etc/my_init.d/startup.sh

# VOLUME for wiki folder . where all the data is loaded from wikipedia. 
VOLUME /config /opt/xowa/wiki

# Expose ports
EXPOSE 8080

# Use baseimage-docker's init system.
CMD ["/sbin/my_init"]
