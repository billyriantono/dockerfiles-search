FROM stackbrew/ubuntu:12.04
MAINTAINER mrlshjjang <mrlshjjang@gmail.com>
RUN (echo "deb http://archive.ubuntu.com/ubuntu/ precise main restricted universe multiverse" > /etc/apt/sources.list && echo "deb http://archive.ubuntu.com/ubuntu/ precise-updates main restricted universe multiverse" >> /etc/apt/sources.list && echo "deb http://archive.ubuntu.com/ubuntu/ precise-backports main restricted universe multiverse" >> /etc/apt/sources.list && echo "deb http://archive.ubuntu.com/ubuntu/ precise-security main restricted universe multiverse" >> /etc/apt/sources.list)
RUN apt-get update

# passwod 설정없이 넘어가기..
ENV DEBIAN_FRONTEND noninteractive

# install openjdk-8-jdk
RUN apt-get install -y openjdk-7-jdk && \
	  apt-get install -y ant && \
	  apt-get clean;

# Fix certificate issues, found as of
# https://bugs.launchpad.net/ubuntu/+source/ca-certificates-java/+bug/983302
RUN apt-get update && \
	apt-get install ca-certificates-java && \
	apt-get clean && \
	update-ca-certificates -f;

# Setup JAVA_HOME, this is useful for docker commandline
ENV JAVA_HOME /usr/lib/jvm/java-7-openjdk-amd64/
RUN export JAVA_HOME

# nginx
RUN apt-get install -y nginx

# uwsgi
RUN apt-get install -y uwsgi

# sshd install
RUN apt-get install -y openssh-server
RUN mkdir /var/run/sshd
RUN echo 'root:root' |chpasswd
RUN sed -ri 's/^PermitRootLogin\s+.*/PermitRootLogin yes/' /etc/ssh/sshd_config
RUN sed -ri 's/UsePAM yes/#UsePAM yes/g' /etc/ssh/sshd_config

# python
RUN apt-get install -y build-essential
RUN apt-get install -y git
RUN apt-get install -y python
RUN apt-get install -y python-dev
RUN apt-get install -y python-setuptools
RUN apt-get install -y python-mysqldb
RUN apt-get install -y sqlite3
RUN apt-get install -y supervisor

# cron
RUN apt-get install -y cron

# etc
RUN apt-get install -y vim
RUN apt-get install -y sudo
RUN apt-get install -y curl
