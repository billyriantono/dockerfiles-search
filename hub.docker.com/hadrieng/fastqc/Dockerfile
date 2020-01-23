FROM hadrieng/docker_base

MAINTAINER Hadrien Gourlé <gourlehadrien@gmail.com>

# install java-1.8
RUN echo 'deb http://ftp.de.debian.org/debian jessie-backports main' \
    >> /etc/apt/sources.list && \
    apt-get update --fix-missing && \
    apt install -y -t jessie-backports \
        libjbzip2-java libcommons-math3-java \
        openjdk-8-jre-headless \
        ca-certificates-java \
        openjdk-8-jdk && \
    /usr/sbin/update-java-alternatives -s java-1.8.0-openjdk-amd64


RUN wget https://launchpad.net/ubuntu/+archive/primary/+files/fastqc_0.11.5+dfsg-3_all.deb && \
    dpkg -i fastqc_0.11.5+dfsg-3_all.deb && \
    apt -y -qq install -f
