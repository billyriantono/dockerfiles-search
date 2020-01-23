FROM ubuntu:15.04

RUN echo "deb http://ppa.launchpad.net/webupd8team/java/ubuntu vivid main"     | tee -a /etc/apt/sources.list && \
    echo "deb-src http://ppa.launchpad.net/webupd8team/java/ubuntu vivid main" | tee -a /etc/apt/sources.list && \
    apt-key adv --keyserver keyserver.ubuntu.com --recv-keys EEA14886 && \
    apt-get update && \
    echo oracle-java7-installer shared/accepted-oracle-license-v1-1 select true | /usr/bin/debconf-set-selections && \
    DEBIAN_FRONTEND=noninteractive apt-get install -y \
      oracle-java7-installer \
      oracle-java7-set-default \
      ca-certificates \
      curl && \
    rm -rdf /var/cache/oracle-jdk7-installer /usr/lib/jvm/java-7-oracle/src.zip
