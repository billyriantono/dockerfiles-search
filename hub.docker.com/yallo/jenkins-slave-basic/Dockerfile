# This Dockerfile is used to build an image containing basic stuff to be used as a Jenkins slave build node.
FROM ubuntu:trusty
MAINTAINER Ervin Varga <ervin.varga@gmail.com>

# Install and configure a basic SSH server
RUN apt-get update &&\
    apt-get install -y openssh-server &&\
    apt-get clean -y && rm -rf /var/lib/apt/lists/* &&\
    sed -i 's|session    required     pam_loginuid.so|session    optional     pam_loginuid.so|g' /etc/pam.d/sshd &&\
    mkdir -p /var/run/sshd

# Install JDK 7 (latest edition)
RUN apt-get update &&\
    apt-get install -y openjdk-7-jdk &&\
    apt-get install -y git &&\
    apt-get install -y \
    ssh \
    python \
    python-pip \
    python-virtualenv &&\    
    apt-get clean -y && rm -rf /var/lib/apt/lists/*

# Set user jenkins to the image
RUN adduser --quiet jenkins &&\
    echo "jenkins:jenkins" | chpasswd

RUN \
    mkdir /home/jenkins/aws && \
    virtualenv /home/jenkins/aws/env && \
    /home/jenkins/aws/env/bin/pip install awscli && \
    echo 'source /home/jenkins/aws/env/bin/activate' >> /home/jenkins/.bashrc && \
    echo 'complete -C aws_completer aws' >> .bashrc

USER jenkins

RUN \
    . /home/jenkins/aws/env/bin/activate && \
    aws configure set preview.cloudfront true && \
    deactivate

USER root

# COPY known_hosts /home/jenkins/.ssh/
# Standard SSH port
EXPOSE 22

CMD ["/usr/sbin/sshd", "-D"]
