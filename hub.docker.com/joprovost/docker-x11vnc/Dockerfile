FROM ubuntu:14.04.3
ENV DEBIAN_FRONTEND noninteractive
ENV HOME /root
RUN apt-get update && apt-get install -y --force-yes --no-install-recommends \
    supervisor xinetd x11vnc xvfb tinywm openbox xdotool wmctrl x11-utils xterm \
    && apt-get autoclean && apt-get autoremove && rm -rf /var/lib/apt/lists/*
