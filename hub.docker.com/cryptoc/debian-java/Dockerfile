# SELECT IMAGE
FROM debian:stretch
MAINTAINER Cryptoc <maintainer@cryptoc.nl>

# Install Java 8
RUN apt-get update && \
    apt-get install software-properties-common dirmngr debconf -y && \
    echo debconf shared/accepted-oracle-license-v1-1 select true | debconf-set-selections && \
    echo debconf shared/accepted-oracle-license-v1-1 seen true | debconf-set-selections && \
    add-apt-repository "deb http://ppa.launchpad.net/webupd8team/java/ubuntu yakkety main" && \
    apt-key adv --keyserver keyserver.ubuntu.com --recv-keys C2518248EEA14886 && \
    apt-get update && \
    apt-get install oracle-java8-installer -y && \
    apt-get clean;

CMD ["java", "-version"]