FROM phusion/baseimage:0.9.17
MAINTAINER Mike O'Driscoll <mike@mikeodriscoll.ca>

ENV DEBIAN_FRONTEND noninteractive
ENV HOME /root

CMD ["/sbin/my_init"]

# Add unifi repo
RUN echo > /etc/apt/sources.list.d/ubnt.list '\n\
## Debian/Ubuntu\n\
# stable => unifi4\n\
# deb http://www.ubnt.com/downloads/unifi/debian unifi4 ubiquiti\n\
deb http://www.ubnt.com/downloads/unifi/debian stable ubiquiti\n\
\n'

# Add Key for unifi
RUN apt-key adv --keyserver keyserver.ubuntu.com --recv C0A52C50

RUN apt-get update -qq && \
apt-get install -qq -y unifi && \
apt-get upgrade -qq && apt-get autoclean && apt-get autoremove && \
rm -rf /var/lib/apt/lists/*

EXPOSE 3478 8080 8081 8443 8843 8880 27117 10001

VOLUME /usr/lib/unifi/data

RUN mkdir /etc/service/unifi
ADD init/unifi.sh /etc/service/unifi/run
RUN chmod +x /etc/service/unifi/run
