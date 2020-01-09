FROM node:0.10

MAINTAINER Kyle Welsby <kyle@mekyle.com>

ENV DEBIAN_FRONTEND noninteractive

RUN echo 'deb http://downloads.sourceforge.net/project/ubuntuzilla/mozilla/apt all main' > /etc/apt/sources.list.d/ubuntuzilla.list
RUN apt-key adv --recv-keys --keyserver keyserver.ubuntu.com C1289A29
RUN apt-get update && apt-get install -y \
    git \
    firefox
