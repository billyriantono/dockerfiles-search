# Parent image
FROM ubuntu

MAINTAINER BAREXTE <barexte@gmail.com>

# Add wine repository
RUN \
  apt update && \
  dpkg --add-architecture i386 && \
  apt install software-properties-common apt-transport-https gnupg wget -y && \
  wget -nc https://dl.winehq.org/wine-builds/winehq.key && \
  apt-key add winehq.key && \
  rm winehq.key && \
  apt-add-repository 'deb https://dl.winehq.org/wine-builds/ubuntu/ bionic main'  && \
  apt update
