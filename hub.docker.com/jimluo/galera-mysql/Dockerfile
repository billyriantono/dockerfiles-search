# Galera Cluster Dockerfile
FROM ubuntu:14.04
MAINTAINER your name <luojinr@guoshengtianfeng.com>

ENV DEBIAN_FRONTEND noninteractive
#ADD sources.list /etc/apt/sources.list

RUN apt-get update
RUN apt-get install -y  software-properties-common
RUN apt-key adv --keyserver keyserver.ubuntu.com --recv BC19DDBA
RUN add-apt-repository 'deb http://releases.galeracluster.com/ubuntu trusty main'

RUN apt-get update
RUN apt-get install -y galera-3 galera-arbitrator-3 mysql-wsrep-5.6 rsync vim

#COPY my.cnf /etc/mysql/my.cnf
ENTRYPOINT ["mysqld"]
