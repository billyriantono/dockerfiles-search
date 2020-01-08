FROM siomiz/chrome

MAINTAINER Jorg Neves Bliesener <jbliesener@bliesener.com>

ENV VNC_PASSWD admin
ENV VNC_WAIT 5
ENV WIDTH 800
ENV HEIGHT 480
ENV COLOR 24
ENV HOME /home/chrome
ENV DISPLAY :1

RUN apt-get update && \
    apt-get clean && \
    rm -rf /var/cache/* /var/log/apt/* /var/lib/apt/lists/* /tmp/*

COPY copyables /

