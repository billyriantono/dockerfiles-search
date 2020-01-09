FROM ubuntu:18.04

RUN apt-get -y update \
    && apt-get -y install \
    vim \
    wget \
    curl \
    unzip \
    build-essential \
    zlib1g-dev \
    #libcurl3 \
    libcurl4 \
    libcurl4-gnutls-dev \
    xterm \
    apt-transport-https \
    software-properties-common \
    && apt-get -y autoremove \
    && apt-get -y autoclean 


RUN dpkg --add-architecture i386 && \
    wget -nc https://dl.winehq.org/wine-builds/winehq.key && \
    apt-key add winehq.key && \
    apt-add-repository https://dl.winehq.org/wine-builds/ubuntu/ && \
    rm *.key

RUN apt-get update && apt-get install -y --install-recommends \
    winehq-stable \
 && rm -rf /var/lib/apt/lists/*
    
RUN wget https://raw.githubusercontent.com/Winetricks/winetricks/master/src/winetricks -O /usr/local/bin/winetricks && \
    chmod +x /usr/local/bin/winetricks

RUN apt-get update && apt-get install -y \
    cabextract \
    dos2unix \
    p7zip-full \
    winbind \
    zip \
 && rm -rf /var/lib/apt/lists/*

ENV WINEARCH win64
ENV WINEPREFIX=/opt/win
RUN winetricks win10

RUN winetricks -q dotnet472
RUN winetricks win10

ENV WINEDEBUG=-all

RUN winetricks win10
RUN wineboot -r

RUN echo $WINEPREFIX

