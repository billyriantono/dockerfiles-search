FROM maven:3-jdk-8
MAINTAINER Christophe Delaitre <cdelaitre@gmail.com>

RUN apt-get update && apt-get install -y openssh-server git
RUN sed -i 's|session    required     pam_loginuid.so|session    optional     pam_loginuid.so|g' /etc/pam.d/sshd
RUN mkdir -p /var/run/sshd
RUN rm -rf /var/lib/apt/lists/* && rm -rf /var/cache/*

RUN adduser --quiet jenkins
RUN echo "jenkins:jenkins" | chpasswd

EXPOSE 22
CMD ["/usr/sbin/sshd", "-D"]
