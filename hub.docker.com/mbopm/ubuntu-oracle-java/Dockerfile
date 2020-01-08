# see http://phusion.github.io/baseimage-docker/
FROM phusion/baseimage:0.9.22
MAINTAINER Manuel Bogner <docker@mbo.pm>
CMD ["/sbin/my_init"]

# update system and install packages
RUN     apt-get update && \
        apt-get dist-upgrade -y && \
        apt-get install -y wget software-properties-common python-software-properties && \
        add-apt-repository -y ppa:webupd8team/java && \
        apt-get update && \
        apt-get dist-upgrade -y && \
        echo debconf shared/accepted-oracle-license-v1-1 select true | debconf-set-selections && \
        echo debconf shared/accepted-oracle-license-v1-1 seen true | debconf-set-selections && \
        apt-get install -y oracle-java8-installer oracle-java8-unlimited-jce-policy && \
        apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

ENV JAVA_HOME /usr/lib/jvm/java-8-oracle
