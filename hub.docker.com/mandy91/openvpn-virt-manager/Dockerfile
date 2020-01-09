FROM ubuntu:18.04
LABEL maintainer "Mandy Schoep <mandyschoep@gmail.com>"

# Audio
RUN apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends alsa-utils libasound2 libasound2-plugins pulseaudio pulseaudio-utils \
  && apt-get clean -y \
  && apt-get autoclean -y \
  && apt-get autoremove -y \
  && rm -rf /tmp/*

# X programs
RUN apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install -y firefox vinagre virt-manager ssh-askpass-gnome ssh-askpass dbus-x11 \
  && apt-get clean -y \
  && apt-get autoclean -y \
  && apt-get autoremove -y \
  && rm -rf /tmp/*

# Base tools
RUN apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install -y openvpn vpnc git vim iputils-ping nmap curl wget sudo rsync  \
  && apt-get clean -y \
  && apt-get autoclean -y \
  && apt-get autoremove -y \
  && rm -rf /tmp/*


RUN groupadd mandy --gid 1000
RUN adduser -uid 1000 -gid 1000 --disabled-password --gecos "" mandy

RUN usermod -a -G sudo mandy
RUN usermod -a -G libvirt mandy
RUN usermod -a -G audio mandy
RUN echo '%sudo ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers

ENV SSH_ASKPASS=/usr/lib/openssh/gnome-ssh-askpass

COPY ./pulse-client.conf /etc/pulse/client.conf

USER mandy

WORKDIR /home/mandy
