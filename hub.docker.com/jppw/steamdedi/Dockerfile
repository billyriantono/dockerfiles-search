FROM ubuntu:14.04

MAINTAINER "Philipp Weber"

ENV DEBIAN_FRONTEND noninteractive

# Install dependencies
RUN apt-get update &&\
apt-get install -y curl lib32gcc1

# Copy scripts
RUN mkdir /opt/scripts

ADD ./scripts/steam-install.sh /opt/scripts/
ADD ./scripts/server.sh /opt/scripts/

RUN chmod +x /opt/scripts/steam-install.sh
RUN chmod +x /opt/scripts/server.sh

# This container will be executable
ENTRYPOINT ["/opt/scripts/steam-install.sh"]
