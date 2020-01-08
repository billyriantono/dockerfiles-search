# Set the base image to ubuntu:16.04
FROM ubuntu:16.04

# File Author / Maintainer
MAINTAINER Yefry Figueroa

#Set TimeZone
RUN echo "Europe/Rome" | tee /etc/timezone
RUN dpkg-reconfigure --frontend noninteractive tzdata

# Set to no tty
ARG DEBIAN_FRONTEND=noninteractive

# Set the locale
RUN locale-gen en_US.UTF-8
ENV LANG=en_US.UTF-8 \
    LANGUAGE=en_US:en \
    LC_ALL=en_US.UTF-8

RUN apt-get update && \
    apt-get -y dist-upgrade && \
    apt-get install -y build-essential && \
    apt-get install -y software-properties-common && \
    apt-get -y install vim mariadb-client inetutils-ping inetutils-telnet byobu curl htop unzip wget && \
    rm -rf /var/lib/apt/lists/*

# Install supplimentary programs
RUN apt-get -y install inetutils-ping && \
    apt-get -y install inetutils-telnet

##Automatic MySQL backup crontab
RUN echo 'SHELL=/bin/bash' >> /var/spool/cron/crontabs/root && \
    echo '30 3 * * *     /backup/00-script/launch_backup.sh' >> /var/spool/cron/crontabs/root

CMD cron -f
