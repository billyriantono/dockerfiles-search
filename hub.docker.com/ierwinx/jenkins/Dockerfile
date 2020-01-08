FROM centos:centos6

USER root

WORKDIR /home/jenkins

RUN yum -y update && yum clean all \
    && yum -y install wget \
    && yum install -y yum-utils \
        device-mapper-persistent-data \
        lvm2 \
    && echo Instala librerias para docker \
    && yum-config-manager \
        --add-repo \
        https://download.docker.com/linux/centos/docker-ce.repo \
    && echo Descarga de docker \
    && yum -y install docker-ce \
    && systemctl enable docker \
    && echo Instalacion Docker finalizada \
    && mkdir /var/lib/jenkins/Respaldos \
    && chown -R jenkins:jenkins /var/lib/jenkins/Respaldos \
    && wget https://downloads.gradle.org/distributions/gradle-4.10.2-bin.zip \
    && mkdir /opt/gradle \
    && unzip -d /opt/gradle gradle-4.10.2-bin.zip \
    && export PATH=$PATH:/opt/gradle/gradle-4.10.2/bin

VOLUME [ "/var/lib/jenkins/Respaldos" ]

CMD systemctl start docker

EXPOSE  8080