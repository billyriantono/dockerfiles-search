# Dockerfile for ZeroTierOne

FROM ubuntu:14.04

MAINTAINER Davide Marquês <nesrait@gmail.com>

RUN apt-get update && apt-get install -y curl

RUN apt-get -y install supervisor && \
    mkdir -p /var/log/supervisor

RUN curl -s https://install.zerotier.com/ | sudo bash && \
    sudo service zerotier-one stop && \
    echo "manual" >> /etc/init/zerotier-one.override && \
    rm /var/lib/zerotier-one/identity.secret && \
    rm /var/lib/zerotier-one/identity.public && \
    mkdir -p /var/lib/zerotier-one/moons.d

# use supervisord to start zerotier
ADD moon/identity.public /var/lib/zerotier-one/identity.public
ADD moon/identity.secret /var/lib/zerotier-one/identity.secret
ADD moon/moon.json /var/lib/zerotier-one/moon.json
ADD moon/00000053e1aa1fda.moon /var/lib/zerotier-one/00000053e1aa1fda.moon
ADD moon/00000053e1aa1fda.moon /var/lib/zerotier-one/moons.d/00000053e1aa1fda.moon
ADD supervisord.conf /etc/supervisor/conf.d/supervisord.conf

EXPOSE 9993/udp

# Default command when starting the container
CMD ["/usr/bin/supervisord", "-c", "/etc/supervisor/conf.d/supervisord.conf"]
