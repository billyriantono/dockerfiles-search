FROM phusion/baseimage:0.10.0
LABEL maintainer="henrik@hedlund.im"

ARG UNIFI_VIDEO_VERSION="3.9.0"
ARG UNIFI_VIDEO_DEB_URL="https://dl.ubnt.com/firmwares/ufv/v${UNIFI_VIDEO_VERSION}/unifi-video.Ubuntu16.04_amd64.v${UNIFI_VIDEO_VERSION}.deb"

ENV DEBIAN_FRONTEND noninteractive
ENV LC_ALL en_US.UTF-8
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US.UTF-8

ADD mongodb.sh /etc/service/mongodb/run
ADD unifi-video.sh /etc/service/unifi-video/run

RUN apt-get update && apt-get upgrade -y && \
    apt-get install -y mongodb-server openjdk-8-jre-headless jsvc sudo && \
    curl -sSL ${UNIFI_VIDEO_DEB_URL} -o /tmp/unifi-video.deb && \
    dpkg -i /tmp/unifi-video.deb && rm /tmp/unifi-video.deb && \
    chmod 500 /etc/service/mongodb/run /etc/service/unifi-video/run && \
    apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

VOLUME ["/var/lib/mongodb", "/var/lib/unifi-video", "/var/log/unifi-video"]
EXPOSE 6666 7080 7442 7443 7445 7446 7447
# Not exposing the MongoDB port 7441 and log directory /var/log/mongodb

# Use baseimage-docker's init system.
CMD ["/sbin/my_init"]
