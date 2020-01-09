FROM balenalib/armv7hf-debian:latest

MAINTAINER eddiepropane

ENV LANG C.UTF-8

RUN [ "cross-build-start" ]

RUN apt-get update && \
    apt-get install -y wget dbus

RUN wget -nv https://tv-mosaic.com/download/01bc9f84ef9aa238c28c9a5c8fbc9653/ -O tvmosaic.tar.gz && tar -xf tvmosaic.tar.gz && \
    dpkg -i tvmosaic-raspberry-linux-armhf_raspbian-1.0.0.deb

RUN rm tvmosaic-raspberry-linux-armhf_raspbian-1.0.0.deb && rm tvmosaic.tar.gz && rm tvmosaic-raspberry-linux-armhf_openelec-1.0.0.tar.gz

ADD /data/recorder_settings.xml /usr/local/bin/tvmosaic/data/config/recorder_settings.xml

ADD /data/tvmosaic.sh /tvmosaic.sh

RUN mkdir /opt-start && mkdir /opt-start/tvmosaic && mkdir /opt-start/TVMosaic && cp -R /usr/local/bin/tvmosaic/* /opt-start/tvmosaic/ && cp -R /opt/TVMosaic/* /opt-start/TVMosaic/

VOLUME [ "/opt/TVMosaic", "/recordings", "/usr/local/bin/tvmosaic" ]

EXPOSE 9270 9271

CMD [ "/tvmosaic.sh" ]

RUN [ "cross-build-end" ]
