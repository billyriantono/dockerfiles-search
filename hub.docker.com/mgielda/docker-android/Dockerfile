FROM ubuntu:16.04

RUN \
  echo 'deb http://ppa.launchpad.net/openjdk-r/ppa/ubuntu xenial main' >> /etc/apt/sources.list && \
  apt-key adv --keyserver keyserver.ubuntu.com --recv-keys DA1A4A13543B466853BAF164EB9B1D8886F44E2A && \
  apt-get update && \
  apt-get -y upgrade && \
  apt-get -y install git-core gnupg flex bison gperf build-essential zip curl zlib1g-dev gcc-multilib g++-multilib libc6-dev-i386 lib32ncurses5-dev x11proto-core-dev libx11-dev lib32z-dev ccache libgl1-mesa-dev libxml2-utils xsltproc unzip python openjdk-7-jdk && \
  curl https://storage.googleapis.com/git-repo-downloads/repo > /usr/bin/repo && \
  chmod a+x /usr/bin/repo
