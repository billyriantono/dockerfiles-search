#######################################################################
# Logitech Media Server
# https://www.mysqueezebox.com/download
#######################################################################

# Base image: https://github.com/phusion/baseimage-docker
FROM phusion/baseimage:0.10.2

# Set correct environment variables
ENV DEBIAN_FRONTEND="noninteractive"
ENV LC_ALL="C.UTF-8" 
ENV LANG="en_US.UTF-8" 
ENV LANGUAGE="en_US.UTF-8" 

# Use baseimage-docker's init system.
CMD ["/sbin/my_init"]

# Upgrading the operating system inside the container
RUN apt-get update && apt-get upgrade -y -o Dpkg::Options::="--force-confold"

# Install Logitech Media Server
RUN apt-get -qq -y update && \
    apt-get -qq -y install curl lame faad flac sox libio-socket-ssl-perl pv && \
    curl -O http://downloads-origin.slimdevices.com/nightly$(curl http://downloads-origin.slimdevices.com/nightly/?ver=7.9 | grep -o '/7.9[^"]*amd64.deb') && \
    dpkg -i *.deb && \
    rm -f *.deb	

# Clean up APT when done.
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
	
# Adding daemon
RUN mkdir /etc/service/lms
COPY lms.sh /etc/service/lms/run
RUN chmod +x /etc/service/lms/run

VOLUME /config /music
EXPOSE 3483 3483/udp 9000 9090