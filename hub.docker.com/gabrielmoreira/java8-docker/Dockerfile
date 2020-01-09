FROM gabrielmoreira/baseimage-docker

RUN \
  echo oracle-java8-installer shared/accepted-oracle-license-v1-1 select true | /usr/bin/debconf-set-selections && \
  echo "deb http://ppa.launchpad.net/webupd8team/java/ubuntu trusty main" | tee /etc/apt/sources.list.d/webupd8team-java.list && \
  echo "deb-src http://ppa.launchpad.net/webupd8team/java/ubuntu trusty main" | tee -a /etc/apt/sources.list.d/webupd8team-java.list && \
  apt-key adv --keyserver keyserver.ubuntu.com --recv-keys EEA14886 && \
  apt-get update && \
  apt-get install -y --no-install-recommends oracle-java8-installer && \
  apt-get clean && \
  apt-get autoclean && \
  apt-get autoremove && \
  rm /var/lib/apt/lists/*_* && \
  rm /usr/lib/jvm/java-8-oracle/*.zip && \
  rm /var/cache/oracle-jdk8-installer/*.tar.gz && \
  rm -Rf /usr/lib/jvm/java-8-oracle/lib/missioncontrol && \
  rm -Rf /usr/lib/jvm/java-8-oracle/lib/visualvm



