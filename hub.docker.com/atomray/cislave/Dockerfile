FROM alexeiled/docker-oracle-xe-11g:latest
MAINTAINER "adam.ramadan@fcc-fac.ca"

RUN uname -a
RUN apt-get install -y python-software-properties
RUN apt-get install -y software-properties-common
RUN apt-get update
RUN add-apt-repository "deb http://archive.ubuntu.com/ubuntu `lsb_release -cs` main universe restricted multiverse"
RUN apt-get update
RUN apt-get install -y mercurial
RUN apt-get install -y openjdk-7-jdk
RUN apt-get install -y xvfb x11-xkb-utils xfonts-100dpi xfonts-75dpi xfonts-scalable xfonts-cyrillic x11-apps
RUN mkdir /build
RUN mkdir /build/workspace
ADD slave.jar /build/
RUN useradd -ms /bin/bash jenkins
RUN chown -R jenkins:jenkins /build
ADD startSlave.sh /root/
RUN chmod 700 /root/startSlave.sh

ENTRYPOINT ["/root/startSlave.sh"]

