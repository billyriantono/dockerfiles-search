FROM ubuntu:18.04

RUN apt update && apt-get install maven software-properties-common -y
RUN apt-add-repository ppa:webupd8team/java
RUN apt-get update
# to automate installation of java8 and remove user interaction during install:
RUN echo oracle-java8-installer shared/accepted-oracle-license-v1-1 select true | /usr/bin/debconf-set-selections
RUN apt-get install oracle-java8-installer -y
