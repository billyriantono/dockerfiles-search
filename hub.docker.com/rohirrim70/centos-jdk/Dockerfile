FROM centos:7

MAINTAINER Christian Klein <christian.klein@base22.com>

ENV JAVA_MAJOR_VERSION=8
ENV JAVA_UPDATE_VERSION=112
ENV JAVA_BUILD_NUMER=15
ENV JAVA_VERSION=1.${JAVA_MAJOR_VERSION}.0_${JAVA_UPDATE_VERSION}
ENV JAVA_HOME=/opt/jdk${JAVA_VERSION}

RUN export JAVA_TARBALL=jdk-${JAVA_MAJOR_VERSION}u${JAVA_UPDATE_VERSION}-linux-x64.tar.gz && \
    # Install tooling
    yum update -y && \
    yum clean all && \
    # install some basic tools
    yum -y install wget net-tools vim && \
    # install java
    cd /opt && \
    curl -j -k -L -H "Cookie: gpw_e24=http%3A%2F%2Fwww.oracle.com%2F; oraclelicense=accept-securebackup-cookie" http://download.oracle.com/otn-pub/java/jdk/${JAVA_MAJOR_VERSION}u${JAVA_UPDATE_VERSION}-b${JAVA_BUILD_NUMER}/${JAVA_TARBALL} | tar xz && \
    
    alternatives --install /usr/bin/java java /opt/${JAVA_VERSION}/bin/java 2 && \
    alternatives --install /usr/bin/javac javac /opt/${JAVA_VERSION}/bin/javac 2 && \
    alternatives --install /usr/bin/jar jar /opt/${JAVA_VERSION}/bin/jar 2 && \

    rm -rf /tmp/* && \
    rm -rf /var/log/*

ENV JRE_HOME=$JAVA_HOME/jre
ENV PATH=$PATH:$JAVA_HOME/bin:$JAVA_HOME/jre/bin

ENV HOME=/root

WORKDIR /root

CMD ["/bin/bash"]