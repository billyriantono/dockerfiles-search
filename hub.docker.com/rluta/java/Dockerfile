FROM ubuntu:trusty
MAINTAINER raphael.luta@gmail.com

RUN echo "deb http://ppa.launchpad.net/webupd8team/java/ubuntu trusty main" > /etc/apt/sources.list.d/webupd8team-java.list
RUN apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys EEA14886
RUN echo oracle-java8-installer shared/accepted-oracle-license-v1-1 select true | /usr/bin/debconf-set-selections
RUN apt-get update -y && apt-get install -y git curl oracle-java8-installer wget subversion unzip supervisor dnsutils tcpdump sysstat strace
RUN apt-get clean && \
  apt-get autoclean && \
  apt-get autoremove && \
  rm /var/lib/apt/lists/*_* && \
  rm /usr/lib/jvm/java-8-oracle/*.zip && \
  rm /var/cache/oracle-jdk8-installer/*.tar.gz && \
  rm -Rf /usr/lib/jvm/java-8-oracle/lib/missioncontrol && \
  rm -Rf /usr/lib/jvm/java-8-oracle/lib/visualvm
RUN cd /usr/local && curl -sL http://dl.bintray.com/groovy/maven/groovy-binary-2.4.1.zip > groovy.zip && unzip groovy.zip && rm groovy.zip && ln -sf groovy-* groovy && ln -sf /usr/local/groovy/bin/groovy bin/groovy
