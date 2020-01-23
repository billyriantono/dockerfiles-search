# https://hub.docker.com/r/nodesource/jessie/tags/
FROM nodesource/jessie:6.7.0

MAINTAINER Fabien FORTON <fabienforton@icloud.com>

# Debugging helpers
##################################################
RUN alias ll='ls -alG'

# Set environment variables
##################################################
ENV DEBIAN_FRONTEND noninteractive
ENV TERM xterm


# Install tools
##################################################
RUN apt-get update; \
    apt-get install -y apt-utils apt-transport-https; \
    apt-get upgrade -y; \
    apt-get install -y locales curl wget; \
    apt-get install -y libnss-mdns avahi-discover libavahi-compat-libdnssd-dev libkrb5-dev; \
    apt-get install -y nano vim

# Install ffmpeg
##################################################
RUN echo 'deb http://www.deb-multimedia.org jessie main non-free' >> /etc/apt/sources.list;
RUN echo 'deb-src http://www.deb-multimedia.org jessie main non-free' >> /etc/apt/sources.list;
RUN apt-get update;
RUN apt-get install deb-multimedia-keyring --force-yes --assume-yes;
RUN apt-get update
RUN apt-get install build-essential libmp3lame-dev libvorbis-dev libtheora-dev libspeex-dev yasm pkg-config libfdk-aac-dev libopenjpeg-dev libx264-dev  --force-yes --assume-yes;
RUN cd /tmp/
RUN mkdir software
RUN cd software
ADD http://ffmpeg.org/releases/ffmpeg-3.2.tar.bz2 /tmp/software/ 
RUN	tar -xvjf /tmp/software/ffmpeg-3.2.tar.bz2 ; 
RUN cd ffmpeg-3.2 \
&& ./configure --enable-gpl --enable-postproc --enable-swscale --enable-avfilter --enable-libmp3lame --enable-libvorbis --enable-libtheora --enable-libx264 --enable-libspeex --enable-shared --enable-pthreads --enable-libopenjpeg --enable-libfdk-aac --enable-nonfree \
&& make \
&& make install \
&& /sbin/ldconfig  ;

# Install tools
##################################################
RUN curl -sL https://deb.nodesource.com/setup_7.x | bash -RUN apt-get install -y nodejsRUN curl -L https://npmjs.org/install.sh | sh
RUN npm install -g homebridge --unsafe-perm
RUN npm install -g  homebridge-camera-ffmpeg
RUN npm install -g  homebridge-eedomus
RUN npm install -g  homebridge-netatmo
RUN npm install -g  homebridge-synology
RUN npm install -g  homebridge-melcloud
RUN npm install -g  homebridge-httpdoor
ADD homebridge-eedomus/index.js /usr/lib/node_modules/homebridge-eedomus/

# Final settings
##################################################


USER root
RUN mkdir -p /var/run/dbus

ADD image/run.sh /root/run.sh

# Run container
##################################################
EXPOSE 5353 51826
CMD ["/root/run.sh"]