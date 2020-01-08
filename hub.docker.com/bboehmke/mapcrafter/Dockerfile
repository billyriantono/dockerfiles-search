FROM debian:jessie

# install mapcrafter
RUN export DEBIAN_FRONTEND=noninteractive && \
    apt-get update && \
    apt-get -y install wget apt-transport-https && \
    echo "deb http://packages.mapcrafter.org/debian jessie main" > /etc/apt/sources.list.d/mapcrafter.list && \
    wget -qO - http://packages.mapcrafter.org/debian/keyring.gpg | apt-key add - && \
    apt-get update && \
    apt-get -y install python imagemagick mapcrafter && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

WORKDIR "/data/"
VOLUME "/data/"

