FROM debian:stretch
ENV DEBIAN_FRONTEND noninteractive
ENV TERM xterm

# Install base environment
RUN apt-get update && apt-get upgrade -y && apt-get install -y --no-install-recommends apt-utils
RUN apt-get -y install \
apt-transport-https \
build-essential \
curl \
cpanminus \
dfu-programmer \
etherwake \
git \
netcat \
perl \
snmp \
snmpd \
sqlite3 \
sudo \
telnet \
usbutils \
vim \
wget && \
apt-get -y install \
libwww-perl \
libsoap-lite-perl \
libxml-parser-lite-perl

EXPOSE 4711

WORKDIR "/opt/fhem/FHEM"

CMD perl 00_SONOS.pm 4711 3 1
