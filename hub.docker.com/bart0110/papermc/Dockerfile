FROM nimmis/java:openjdk-8-jdk

# PAPERMC_HOME         default directory for PAPERMC-server
# PAPERMC_VER          default minecraft version to compile
# PAPERMC_AUTORESTART  set to yes to restart if minecraft stop command is executed
ENV PAPERMC_HOME=/minecraft \
    PAPERMC_VER=latest \
    PAPERMC_AUTORESTART=yes

# add extra files needed
COPY rootfs /

RUN apt-get update

# upgrade OS
RUN apt-get -y dist-upgrade

# Make info file about this build
RUN printf "Build of bart0110/PAPERMC, date: %s\n"  `date -u +"%Y-%m-%dT%H:%M:%SZ"` > /etc/BUILDS/PAPERMC

# install application
RUN apt-get install -y wget git jq

# Make special user for minecraft to run in
RUN /usr/sbin/useradd -s /bin/bash -d /minecraft -m minecraft

# remove apt cache from image
RUN apt-get clean all

# Docker Healthcheck:
HEALTHCHECK CMD /usr/local/bin/healthcheck.sh

# expose minecraft port
EXPOSE 25565


