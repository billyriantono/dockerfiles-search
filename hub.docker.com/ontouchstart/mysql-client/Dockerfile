FROM ubuntu:14.04
MAINTAINER Sam Liu <ontouchstart@gmail.com>

RUN apt-get update -y
RUN apt-get upgrade -y

RUN apt-get -y install mysql-client
ADD work work
WORKDIR work
