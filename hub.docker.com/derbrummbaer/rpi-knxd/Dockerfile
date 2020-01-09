############################################################
# Dockerfile zum erstellen eines Dockercontainers für
# knxd
############################################################

############################################################
# Argument Variables from YAML File
############################################################

FROM derbrummbaer/rpi-raspbian:stretch

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

RUN apt-get update
RUN apt-get dist-upgrade -qy

############################################################
# Install Software: knxd
############################################################

RUN apt-get install -qy git-core init-system-helpers
RUN apt-get install -qy build-essential wget cdbs debhelper libusb-1.0-0-dev libsystemd-dev 
RUN apt-get install -qy autotools-dev autoconf automake libtool pkg-config dh-systemd libev-dev cmake 


RUN git clone -b stable https://github.com/knxd/knxd.git

RUN cd knxd \
     && ./bootstrap.sh \
     && ./configure --disable-systemd --enable-tpuart --enable-usb --enable-eibnetipserver --enable-eibnetip --enable-eibnetserver --enable-eibnetiptunnel \
     && mkdir -p src/include/sys && ln -s /usr/lib/bcc/include/sys/cdefs.h src/include/sys \
     && make \
     && make install

############################################################
# Remove Apt Data
############################################################

RUN apt-get remove build-essential debhelper autotools-dev autoconf automake cmake pkg-config git-core -qy \
  && apt-get autoremove -qy \
  && apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN rm -R ./knxd

############################################################
# Copy External Data
############################################################

############################################################
# Copy Start Scripts
############################################################

COPY scripte/entrypoint.sh /entrypoint.sh
RUN chmod +x /entrypoint.sh

############################################################
# Folders needed
############################################################

############################################################
# Ports needed
############################################################

EXPOSE 3672 6720

############################################################
############################################################
# USE CROSS-BUILD for Raspberry PI Images
############################################################
############################################################

RUN [ "cross-build-end" ]

############################################################
# Container Start
############################################################

ENTRYPOINT ["/entrypoint.sh"]
CMD ["knxd"]