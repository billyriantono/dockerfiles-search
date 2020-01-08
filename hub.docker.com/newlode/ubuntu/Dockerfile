FROM ubuntu:latest
MAINTAINER Newlode <tech@newlode.io>

# Ne pas poser de questions debconf lors des phases d'installation
ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update && apt-get install -y locales && rm -rf /var/lib/apt/lists/* \
    && localedef -i fr_FR -c -f UTF-8 -A /usr/share/locale/locale.alias fr_FR.UTF-8
ENV LANG fr_FR.utf8


