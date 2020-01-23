# This Dockerfile is used to build an image containing basic stuff to be used as a Jenkins slave build node.
FROM ubuntu:xenial
MAINTAINER Bilal Baqar <mbilalbaqar@gmail.com>

ENV DEBIAN_FRONTEND noninteractive

# In case you need proxy
#RUN echo 'Acquire::http::Proxy "http://127.0.0.1:8080";' >> /etc/apt/apt.conf

RUN apt-get clean &&\
    apt-get update &&\
    apt-get install -y -o Dpkg::Options::="--force-confnew" --no-install-recommends locales &&\
    apt-get install -y -o Dpkg::Options::="--force-confnew" --no-install-recommends apt-utils

RUN locale-gen en_US.UTF-8

# Add locales after locale-gen as needed
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en
ENV LC_ALL en_US.UTF-8


# Upgrade packages on image
# Preparations for sshd
RUN apt-get -q update &&\
    apt-get -q upgrade -y -o Dpkg::Options::="--force-confnew" --no-install-recommends &&\
    apt-get -q install -y -o Dpkg::Options::="--force-confnew" --no-install-recommends openssh-server &&\
    apt-get -q install -y -o Dpkg::Options::="--force-confnew" --no-install-recommends git &&\
    apt-get -q install -y -o Dpkg::Options::="--force-confnew" --no-install-recommends curl &&\
    apt-get -q install -y -o Dpkg::Options::="--force-confnew" --no-install-recommends zip &&\
    apt-get -q install -y -o Dpkg::Options::="--force-confnew" --no-install-recommends wget &&\
    apt-get -q install -y -o Dpkg::Options::="--force-confnew" --no-install-recommends unzip &&\
    apt-get -q autoremove &&\
    apt-get -q clean -y && rm -rf /var/lib/apt/lists/* && rm -f /var/cache/apt/*.bin &&\
    sed -i 's|session    required     pam_loginuid.so|session    optional     pam_loginuid.so|g' /etc/pam.d/sshd &&\
    mkdir -p /var/run/sshd


# Install JDK 8 (latest edition)
RUN apt-get -q update &&\
    apt-get -q install -y -o Dpkg::Options::="--force-confnew" --no-install-recommends software-properties-common &&\
    add-apt-repository -y ppa:openjdk-r/ppa &&\
    apt-get -q update &&\
    apt-get -q install -y -o Dpkg::Options::="--force-confnew" --no-install-recommends openjdk-8-jre-headless &&\
    apt-get -q clean -y && rm -rf /var/lib/apt/lists/* && rm -f /var/cache/apt/*.bin

# Set user jenkins to the image
RUN useradd -m -d /home/jenkins -s /bin/sh jenkins &&\
    echo "jenkins:jenkins" | chpasswd

RUN /usr/bin/ssh-keygen -A
RUN mkdir /home/jenkins/.ssh
RUN chown -R jenkins /home/jenkins
RUN chgrp -R jenkins /home/jenkins
RUN chmod 700 /home/jenkins/.ssh

RUN echo "jenkins  ALL=(ALL)  ALL" >> etc/sudoers

# setting interactive mode
ENV DEBIAN_FRONTEND teletype

# Standard SSH port
EXPOSE 22

# Default command
CMD ["/usr/sbin/sshd", "-D"]
