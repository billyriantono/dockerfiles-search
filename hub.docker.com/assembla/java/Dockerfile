FROM assembla/ubuntu
MAINTAINER Artiom Di <kron82@gmail.com>

RUN echo "deb http://ppa.launchpad.net/webupd8team/java/ubuntu trusty main" | \
    tee /etc/apt/sources.list.d/webupd8team-java.list && \
    apt-key adv --keyserver keyserver.ubuntu.com --recv-keys EEA14886 && \
    apt-get update && \
    echo "oracle-java8-installer shared/accepted-oracle-license-v1-1 select true" | \
    /usr/bin/debconf-set-selections && \
    DEBIAN_FRONTEND=noninteractive apt-get install -y --force-yes \
        oracle-java8-installer oracle-java8-set-default && \
    rm -rf /var/cache/oracle-jdk8-installer && \
    update-alternatives --display java && \
    rm -rf /var/lib/apt/lists/* && \
    apt-get clean

ENV JAVA_HOME /usr/lib/jvm/java-8-oracle
CMD ["java"]
