FROM ubuntu:xenial
MAINTAINER James Grant <james@queeg.org>

ENV DEBIAN_FRONTEND noninteractive

# Update Image
RUN apt-get update &&\
    apt-get upgrade -y &&\
    rm -rf /var/lib/apt/lists/* /var/cache/apt/*.bin

# Docker
RUN apt-get update &&\
    apt-get install -y apt-transport-https ca-certificates curl lxc iptables &&\
    echo deb https://apt.dockerproject.org/repo ubuntu-xenial main > /etc/apt/sources.list.d/docker.list &&\
    apt-key adv --keyserver hkp://p80.pool.sks-keyservers.net:80 --recv-keys 58118E89F3A912897C070ADBF76221572C52609D &&\
    apt-get update &&\
    apt-get install -y docker-engine &&\
    rm -rf /var/lib/apt/lists/* /var/cache/apt/*.bin

# Java 8
RUN apt-get update &&\
    apt-get install -y software-properties-common debconf &&\
    echo oracle-java8-installer shared/accepted-oracle-license-v1-1 select true | debconf-set-selections &&\
    add-apt-repository -y ppa:webupd8team/java && \
    apt-get update &&\
    apt-get install -y oracle-java8-installer &&\
    rm -rf /var/lib/apt/lists/* /var/cache/apt/*.bin /var/cache/oracle-jdk8-installer

# Maven
RUN apt-get update &&\
    apt-get install -y maven &&\
    rm -rf /var/lib/apt/lists/* /var/cache/apt/*.bin

# SSh Server
RUN apt-get update &&\
    apt-get install -y openssh-server &&\
    sed -i 's|session    required     pam_loginuid.so|session    optional     pam_loginuid.so|g' /etc/pam.d/sshd &&\
    mkdir -p /var/run/sshd &&\
    rm -rf /var/lib/apt/lists/* /var/cache/apt/*.bin

ADD wrapdocker /usr/local/bin/wrapdocker
VOLUME /var/lib/docker

ENV LANG en_GB.UTF-8
ENV LANGUAGE en_GB:en
ENV LC_ALL en_GB.UTF-8
ENV JAVA_HOME /usr/lib/jvm/java-8-oracle
RUN locale-gen ${LANG}

# Set user jenkins to the image
RUN useradd -m -d /home/jenkins -s /bin/sh jenkins &&\
    usermod -a -G docker jenkins &&\
    echo "jenkins:jenkins" | chpasswd

RUN curl --create-dirs -sSLo /usr/share/jenkins/slave.jar http://repo.jenkins-ci.org/public/org/jenkins-ci/main/remoting/2.52/remoting-2.52.jar &&\
    chmod 755 /usr/share/jenkins &&\
    chmod 644 /usr/share/jenkins/slave.jar

ADD jenkins-slave /usr/local/bin/jenkins-slave
ADD ssh_config /etc/ssh/ssh_config

VOLUME /home/jenkins
WORKDIR /home/jenkins
#USER jenkins

CMD ["jenkins-slave"]

