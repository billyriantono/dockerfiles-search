# Factorio clusterio Dockerfile
# Copyright Gerkiz@nvfs.se
#
# Copying and distribution of this file, with or without modification,
# are permitted in any medium without royalty provided the copyright
# notice and this notice are preserved.  This file is offered as-is,
# without any warranty.
#
# Description: Factorio docker image for Pterodactyl. 

FROM ubuntu:18.04

LABEL maintainer="Gerkiz <Gerkiz@nvfs.se>"

###
### Add the user.
### Pterodactyl apparently needs a user to run this...
###
RUN apt update \
	&& apt install -y sudo curl \
	&& adduser --home /home/container --disabled-password --gecos "" container \
	&& echo "container:container" | chpasswd \
	&& usermod -a -G sudo container

###
### Install the dumb handler.
### Rewrites the SIGKILL signals.
###
RUN apt install psmisc dumb-init

###
### Download node and other utilities that are required by Clusterio.
###	
RUN cd /home/container \
	&& curl -sL https://deb.nodesource.com/setup_10.x | sudo -E bash - \
	&& apt install -y nodejs \
    && apt install -y git tar bash python-dev xz-utils p7zip-full wget build-essential gdb

###
### Upgrade existing packages.
###
RUN apt update \	
    && apt upgrade -y

COPY ./entrypoint.sh /entrypoint.sh
RUN chmod +x /entrypoint.sh
	
USER container
ENV  USER container
ENV  HOME /home/container/
WORKDIR /home/container/
	
CMD ["/usr/bin/dumb-init", "-v", "--single-child", "--rewrite", "15:2", "/entrypoint.sh"]
