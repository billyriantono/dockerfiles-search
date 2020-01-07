FROM dockeredcom/debian-stretch-gpg

MAINTAINER Yves Vindevogel (yves.vindevogel@asynchrone.com / yves.vindevogel@dockered.com)

ARG DEBIAN_FRONTEND=noninteractive
ARG JDK_BUILD=8u181-b13
ARG DOWNLOAD_LOCATION=http://download.oracle.com/otn-pub/java/jdk/8u181-b13/96a7b8442fe848ef90c96a2fad6ed6d1/jdk-8u181-linux-x64.tar.gz
ARG SDKMAN_DIR=/opt/sdkman

ENV SHELL=/bin/bash

WORKDIR /tmp

COPY ./java.sh /etc/profile.d/java.sh

RUN set -x && \ 
    chmod +x /etc/profile.d/java.sh && \ 
    echo "[[ -s /etc/profile.d/java.sh ]] && source /etc/profile.d/java.sh" >> /root/.bashrc && \ 
    apt-get update --yes && \ 
    apt-get upgrade --yes && \ 
    apt-get install unzip zip curl ca-certificates --yes --no-install-recommends && \ 
    curl --header "Cookie:oraclelicense=accept-securebackup-cookie" --location $DOWNLOAD_LOCATION --output /tmp/jdk.tar.gz && \ 
    mkdir -p /opt/oracle-jdk && \ 
    tar -zxf /tmp/jdk.tar.gz -C /opt/oracle-jdk --strip 1 && \ 
    rm -f /tmp/jdk.tar.gz && \ 
    curl -s "https://get.sdkman.io" | bash && \ 
    bash -l -c "sdk install java $JDK_BUILD /opt/oracle-jdk" && \ 
    rm -f /opt/oracle-jdk/javafx-src.zip && \ 
    rm -f /opt/oracle-jdk/src.zip && \ 
    rm -f /opt/oracle-jdk/THIRDPARTYLICENSEREADME-JAVAFX.txt && \ 
    rm -f /opt/oracle-jdk/THIRDPARTYLICENSEREADME.txt && \ 
    apt-get autoremove --yes && \ 
    apt-get clean && \ 
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

CMD [ "/bin/bash" ]
