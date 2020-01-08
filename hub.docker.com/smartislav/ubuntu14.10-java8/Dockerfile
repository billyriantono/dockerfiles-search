FROM ubuntu:14.10

MAINTAINER Ilya Epifanov <elijah.epifanov@gmail.com>

RUN apt-get update
RUN apt-get -y upgrade
RUN apt-get -y install wget
RUN /usr/bin/wget 'http://deb.smslv.ru/repo.key' -O - | apt-key add -
RUN echo 'deb http://deb.smslv.ru/ ubuntu main' > /etc/apt/sources.list.d/deb.smslv.ru.list
RUN apt-get update
RUN apt-get install -y oracle-java8-jdk
RUN update-java-alternatives -s java-8-oracle || /bin/true
RUN apt-get install -y ca-certificates-java
RUN ln -sfT /etc/ssl/certs/java/cacerts /etc/java-8-oracle/security/cacerts

RUN apt-get clean
RUN rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
