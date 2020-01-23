FROM phusion/baseimage:0.9.11

MAINTAINER aptalca

RUN export DEBCONF_NONINTERACTIVE_SEEN=true DEBIAN_FRONTEND=noninteractive && \
apt-get update && \
apt-get install -y \
wget \
lxde \
xrdp
