FROM node:9.8-stretch

MAINTAINER Marco Raddatz

# Set environment variables
ENV DEBIAN_FRONTEND noninteractive
ENV TERM xterm

# Install dependencies and tools
RUN echo "deb http://www.deb-multimedia.org stretch main non-free" >> /etc/apt/sources.list
RUN apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 5C808C2B65558117

RUN apt-get update

RUN apt-get -y install ffmpeg libfdk-aac-dev libfaac-dev

RUN apt-get install -y apt-utils apt-transport-https; \
    apt-get install -y curl wget; \
    apt-get install -y libnss-mdns avahi-discover libavahi-compat-libdnssd-dev libkrb5-dev; \
    apt-get install -y ffmpeg libfdk-aac-dev libfaac-dev; \
    apt-get install -y nano vim

# Install latest Homebridge
# -------------------------------------------------------------------------
# You can force a specific version by setting HOMEBRIDGE_VERSION
# See https://github.com/marcoraddatz/homebridge-docker#homebridge_version
# -------------------------------------------------------------------------
RUN npm install -g homebridge --unsafe-perm

#Install ffmpeg via sh script
#ADD install_ffmpeg_ubuntu.sh /tmp/
#RUN chmod +x /tmp/install_ffmpeg_ubuntu.sh
#RUN /tmp/install_ffmpeg_ubuntu.sh 
#RUN rm /tmp/install_ffmpeg_ubuntu.sh

# MISC settings
COPY avahi-daemon.conf /etc/avahi/avahi-daemon.conf

USER root
RUN mkdir -p /var/run/dbus

ADD image/run.sh /root/run.sh

# Run container
EXPOSE 5353 51826
CMD ["/root/run.sh"]
