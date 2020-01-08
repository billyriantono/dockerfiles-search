FROM debian:jessie

MAINTAINER vmedek <vaclav.medek@aevi.com>

ADD local_policy.jar /opt/
ADD US_export_policy.jar /opt/
RUN echo deb "http://http.debian.net/debian jessie-backports main" >>/etc/apt/sources.list.d/backports.list && \
    echo "CET" > /etc/timezone && dpkg-reconfigure -f noninteractive tzdata && \    
    apt-get update && \
    apt-get upgrade -y && \
    apt-get install vim dnsutils telnet software-properties-common -y && \
    apt-get install -y redis-tools && \
    add-apt-repository "deb http://ppa.launchpad.net/webupd8team/java/ubuntu xenial main" && \
    apt-get update && \
    echo debconf shared/accepted-oracle-license-v1-1 select true | debconf-set-selections  && \
    echo debconf shared/accepted-oracle-license-v1-1 seen true | debconf-set-selections  && \
    DEBIAN_FRONTEND=noninteractive  apt-get install -y --force-yes oracle-java8-installer oracle-java8-set-default && \
    rm -rf /var/cache/oracle-jdk8-installer  && \
    apt-get clean  && \
    rm -rf /var/lib/apt/lists/* && \
    mv /opt/*.jar /usr/lib/jvm/java-8-oracle/jre/lib/security/

VOLUME /etc/timezone:/etc/localtime

ENV JAVA_HOME /usr/lib/jvm/java-8-oracle

CMD ["/bin/bash"]
