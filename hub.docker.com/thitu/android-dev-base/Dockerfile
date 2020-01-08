FROM vixns/java8

RUN echo 'debconf debconf/frontend select Noninteractive' | debconf-set-selections

##
## Required by android-sdk
##
RUN dpkg --add-architecture i386 && \
  apt-get update -q -qq -y && \
  apt-get install -q -qq -y xorg libc6:i386 libncurses5:i386 libstdc++6:i386 lib32z1 libx11-6 libglu1-mesa libx11-6:i386 libglu1-mesa:i386 libpulse0 libpulse0:i386 awscli git docker gradle && \
  rm -rf /var/lib/apt/lists/* && \
  apt-get autoremove -y && \
  apt-get clean

ENV SHELL /bin/bash
ENV DISPLAY :0
ENV TERM linux
