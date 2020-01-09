FROM ubuntu
MAINTAINER Kalle R. Møller <docker@k-moeller.dk>

ARG DEBIAN_FRONTEND=noninteractive
ARG WINE_GECKO_VERSION=2.40
ARG WINE_MONO_VERSION=4.5.6

# Updating and upgrading a bit.
RUN apt-get update -y && \
   apt-get install -y wget && \
   mkdir -p /usr/share/wine/gecko && \
   wget "http://dl.winehq.org/wine/wine-gecko/${WINE_GECKO_VERSION}/wine_gecko-${WINE_GECKO_VERSION}-x86.msi" -O /usr/share/wine/gecko/wine_gecko-${WINE_GECKO_VERSION}-x86.msi && \
   chmod +x /usr/share/wine/gecko/wine_gecko-${WINE_GECKO_VERSION}-x86.msi && \
   wget "http://dl.winehq.org/wine/wine-gecko/${WINE_GECKO_VERSION}/wine_gecko-${WINE_GECKO_VERSION}-x86_64.msi" -O /usr/share/wine/gecko/wine_gecko-${WINE_GECKO_VERSION}-x86_64.msi && \
   chmod +x /usr/share/wine/gecko/wine_gecko-${WINE_GECKO_VERSION}-x86_64.msi && \
   mkdir -p /usr/share/wine/mono && \
   wget "http://dl.winehq.org/wine/wine-mono/${WINE_MONO_VERSION}/wine-mono-${WINE_MONO_VERSION}.msi" -O /usr/share/wine/mono/wine-mono-${WINE_MONO_VERSION}.msi && \
   chmod +x /usr/share/wine/mono/wine-mono-${WINE_MONO_VERSION}.msi && \
   apt-get remove -y --purge wget && \
   apt-get autoremove -y --purge && \
   apt-get clean -y  && \
   rm -rf /tmp/* /var/tmp/* /var/lib/apt/lists/*
   
RUN dpkg --add-architecture i386 && \
    apt-get update -y && \
    apt-get install -y --no-install-recommends software-properties-common && \
	
# Adding required ppas: graphics drivers and wine.
   add-apt-repository ppa:ubuntu-wine/ppa && \
   apt-get update -y && \

# Installation of wine, winetricks and its utilities and temporary xvfb to install latest winetricks and its tricks during docker build.
  apt-get install -y --no-install-recommends wine1.8 winetricks xvfb winbind && \
  
# Cleaning
  apt-get remove -y --purge software-properties-common && \
  apt-get autoremove -y --purge && \
  apt-get clean -y  && \
  rm -rf /tmp/* /var/tmp/* /var/lib/apt/lists/*
  
RUN useradd -u 1001 -d /home/wine -m -s /bin/bash wine && \
    mkdir /tmp/.X11-unix && \
    chmod 1777 /tmp/.X11-unix
    
ENV HOME=/home/wine \
    WINEPREFIX=/home/wine/.wine \
    WINEARCH=win32

WORKDIR /home/wine
USER wine
