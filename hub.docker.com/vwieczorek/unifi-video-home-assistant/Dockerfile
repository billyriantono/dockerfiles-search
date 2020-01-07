FROM phusion/baseimage:0.11
MAINTAINER vwieczorek

# Set correct environment variables
ENV HOME /root
ENV DEBIAN_FRONTEND noninteractive
ENV LC_ALL C.UTF-8
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US.UTF-8

RUN apt-get update && \
  apt-get install -y apt-utils && \
  apt-get upgrade -y -o Dpkg::Options::="--force-confold" && \
  apt-get install -y inotify-tools mosquitto-clients
  
VOLUME ["/var/lib/unifi-video"]

CMD /var/lib/unifi-video/unifi-video-mqtt/unifi-video-mqtt-multiple.sh
