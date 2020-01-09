FROM centos:7

MAINTAINER Takaaki Hirayama dev.takaaki.hirayama@gmail.com

RUN yum install -y openssh-server java-1.8.0-openjdk java-1.8.0-openjdk-devel

EXPOSE 22

RUN groupadd jenkins && useradd -d /home/jenkins -g jenkins -m jenkins

RUN mkdir /home/jenkins/.ssh
COPY id_rsa.pub /home/jenkins/.ssh/authorized_keys
RUN chown -R jenkins:jenkins /home/jenkins/.ssh \
 && chmod 700 /home/jenkins/.ssh \
 && chmod 600 /home/jenkins/.ssh/*

RUN ssh-keygen -A