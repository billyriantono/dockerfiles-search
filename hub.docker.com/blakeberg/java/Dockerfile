FROM ubuntu:14.04.1
# first line must be base image in FROM for automatic build!
#
# Official Ubuntu base image
# 
# Oracle Java SE Development Kit 6u45
# http://www.oracle.com/technetwork/java/javase/downloads/java-se-archive-license-1382604.html
#
# build context size: 0MB
# image size: 	491MB
#
MAINTAINER Bjoern Lakeberg <bjoern.lakeberg@technik-emden.de>

# load packages and install ssh server
RUN apt-get install -y openssh-server
RUN mkdir /var/run/sshd
RUN echo 'root:admin' | chpasswd
RUN sed -i 's/PermitRootLogin without-password/PermitRootLogin yes/' /etc/ssh/sshd_config
RUN sed 's@session\s*required\s*pam_loginuid.so@session optional pam_loginuid.so@g' -i /etc/pam.d/sshd
RUN echo "export VISIBLE=now" >> /etc/profile

# load packages and install java
RUN apt-get install -y software-properties-common
RUN \
  echo oracle-java6-installer shared/accepted-oracle-license-v1-1 select true | debconf-set-selections && \
  add-apt-repository -y ppa:webupd8team/java && \
  apt-get update && \
  apt-get install -y oracle-java6-installer && \
  rm -rf /var/lib/apt/lists/* && \
  rm -rf /var/cache/oracle-jdk6-installer

# define commonly used variables for java and ant
ENV JAVA_HOME /usr/lib/jvm/java-6-oracle

# define and expose ports for ssh
EXPOSE 22

# start ssh
CMD /usr/sbin/sshd -D
