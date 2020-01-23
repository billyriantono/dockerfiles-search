FROM ubuntu:cosmic

MAINTAINER bilbao.goyoaga@gmail.com

ARG DISPLAY=${DISPLAY:-":0.0"}
ENV DISPLAY=${DISPLAY}

USER root

## ---- X11 ----
RUN apt-get update && \
    # apt-get install -y sudo xauth xorg openbox && \
    apt-get install -y sudo xauth xorg fluxbox && \
    apt-get install -y libxext-dev libxrender-dev libxtst-dev firefox && \
    apt-get install -y apt-transport-https ca-certificates libcurl3-gnutls && \
    apt-get install -y apt-utils packagekit-gtk3-module libcanberra-gtk3-module && \
    apt-get install -y dbus-x11 && \
    apt-get install -y xdg-utils --fix-missing && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*
