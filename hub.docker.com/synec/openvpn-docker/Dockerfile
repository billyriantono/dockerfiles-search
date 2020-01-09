# Smallest base image
FROM alpine:3.8

MAINTAINER John Felten<john.felten@gmail.com>

ADD VERSION .

# Install needed packages
RUN apk update && apk add openssl easy-rsa openvpn iptables bash

RUN rm -rf /tmp/* /var/tmp/* /var/cache/apk/* /var/cache/distfiles/*

# Configure tun
RUN mkdir -p /dev/net 

RUN echo 'net.ipv4.ip_forward=1' >> /etc/sysctl.d/00-alpine.conf
