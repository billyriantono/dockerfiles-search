# DOCKER-VERSION 18.09.2
# DESCRIPTION    

# Pull base image
FROM ubuntu:18.04

#========================
# Miscellaneous packages
# Includes minimal runtime used for executing non GUI Java programs
#========================
RUN apt-get update -qqy \
  && apt-get -qqy --no-install-recommends install \
    sudo \
    gnupg \
    ca-certificates \
    unzip \
    wget \
    tzdata \
    locales \
    maven \
  && rm -rf /var/lib/apt/lists/*

#========================================
# Add normal user with passwordless sudo
#========================================
RUN sudo useradd seluser --shell /bin/bash --create-home \
  && sudo usermod -a -G sudo seluser \
  && echo 'ALL ALL = (ALL) NOPASSWD: ALL' >> /etc/sudoers \
  && echo 'seluser:secret' | chpasswd

#============================
# Some configuration options
#============================
ENV SCREEN_WIDTH 1920
ENV SCREEN_HEIGHT 1080
ENV SCREEN_DEPTH 24
ENV DISPLAY :0

#===============
# OpenJDK8
#===============
RUN apt-get update -qqy \
  && apt-get install -qqy software-properties-common \
  && add-apt-repository ppa:openjdk-r/ppa \
  && apt-get update -qqy \
  && apt-get -qqy install openjdk-8-jdk \
  && rm -rf /var/lib/apt/lists/*

#===============
# Google Chrome
#===============

# Install latest
RUN wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | apt-key add - \
  && echo "deb http://dl.google.com/linux/chrome/deb/ stable main" >> /etc/apt/sources.list.d/google-chrome.list \
  && apt-get update -qqy \
  && apt-get -qqy install \
    google-chrome-stable \
  && rm /etc/apt/sources.list.d/google-chrome.list \
  && rm -rf /var/lib/apt/lists/*

# RUN apt-get update -qqy \
#   && apt-get -qqy install \
#     fonts-liberation \
#     libappindicator3-1 \
#     libgtk-3-0 \
#     libxss1 \
#     xdg-utils\ 
#   && rm -rf /var/lib/apt/lists/*

# RUN wget -q http://dl.google.com/linux/chrome/deb/pool/main/g/google-chrome-stable/google-chrome-stable_75.0.3770.142-1_amd64.deb \
#   && dpkg -i google-chrome-stable_75.0.3770.142-1_amd64.deb \
#   && apt-mark hold google-chrome-stable \
#   dpkg -s google-chrome-stable

#=================================
# Chrome Launch Script Modication
#=================================
COPY chrome_launcher.sh /opt/google/chrome/google-chrome
RUN chmod +x /opt/google/chrome/google-chrome

# USER root

#==============
# VNC and Xvfb
#==============
RUN apt-get update -qqy \
  && apt-get -qqy install \
    xvfb \
  && rm -rf /var/lib/apt/lists/*

#=====
# VNC
#=====
RUN apt-get update -qqy \
  && apt-get -qqy install \
    x11vnc \
  && rm -rf /var/lib/apt/lists/* \
  && mkdir -p ~/.vnc \
  && x11vnc -storepasswd secret ~/.vnc/passwd

#=================
# Locale settings
#=================
ENV LANGUAGE en_US.UTF-8
ENV LANG en_US.UTF-8
RUN locale-gen en_US.UTF-8 \
  && dpkg-reconfigure --frontend noninteractive locales \
  && apt-get update -qqy \
  && apt-get -qqy --no-install-recommends install \
    language-pack-en \
  && rm -rf /var/lib/apt/lists/*

#=======
# Fonts
#=======
RUN apt-get update -qqy \
  && apt-get -qqy --no-install-recommends install \
    fonts-ipafont-gothic \
    xfonts-100dpi \
    xfonts-75dpi \
    xfonts-cyrillic \
    xfonts-scalable \
  && rm -rf /var/lib/apt/lists/*

#=========
# fluxbox
# A fast, lightweight and responsive window manager
#=========
RUN apt-get update -qqy \
  && apt-get -qqy install \
    fluxbox \
  && rm -rf /var/lib/apt/lists/*

#==============================
# Azure CLI
#==============================

RUN apt-get update -qqy \
  && apt-get -qqy install \
    curl apt-transport-https lsb-release gnupg \
  && curl -sL https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor | sudo tee /etc/apt/trusted.gpg.d/microsoft.asc.gpg > /dev/null \
  && AZ_REPO=$(lsb_release -cs) \
  && echo "deb [arch=amd64] https://packages.microsoft.com/repos/azure-cli/ $AZ_REPO main" | sudo tee /etc/apt/sources.list.d/azure-cli.list \
  && apt-get update -qqy \
  && apt-get -qqy install \
    azure-cli \
  && rm -rf /var/lib/apt/lists/*

#==============================
# Scripts to run 
#==============================
COPY entry_point.sh /opt/bin/entry_point.sh
RUN chmod +x /opt/bin/entry_point.sh

EXPOSE 5900

# USER seluser

ENTRYPOINT ["/opt/bin/entry_point.sh"]
