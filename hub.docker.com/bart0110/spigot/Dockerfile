FROM nimmis/java:openjdk-8-jdk

MAINTAINER nimmis <kjell.havneskold@gmail.com>

# SPIGOT_HOME         default directory for SPIGOT-server
# SPIGOT_VER          default minecraft version to compile
# SPIGOT_AUTORESTART  set to yes to restart if minecraft stop command is executed
ENV SPIGOT_HOME=/minecraft \
    SPIGOT_VER=latest \
    SPIGOT_AUTORESTART=yes

# add extra files needed
COPY rootfs /

RUN apt-get update

# upgrade OS
RUN apt-get -y dist-upgrade

# Make info file about this build
RUN printf "Build of bart0110/spigot:latest, date: %s\n"  `date -u +"%Y-%m-%dT%H:%M:%SZ"` > /etc/BUILDS/spigot

# install application
RUN apt-get install -y wget git

# Make special user for minecraft to run in
RUN /usr/sbin/useradd -s /bin/bash -d /minecraft -m minecraft

# remove apt cache from image
RUN apt-get clean all

# Docker Healthcheck:
HEALTHCHECK CMD /usr/local/bin/healthcheck.sh

# expose minecraft port
EXPOSE 25565


