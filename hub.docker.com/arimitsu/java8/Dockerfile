# clenup
# docker rm $(docker ps -a -q) ; docker rmi arimitsu/java8
# docker images | awk '{if ($2 ~ "<none>") print $3}' | xargs docker rmi

# build
# docker build -t arimitsu/java8 .

# run
# docker run -it arimitsu/java8 /bin/bash

FROM ubuntu:14.04
MAINTAINER Y.Arimitsu<arimitu@ouk.jp>

# 日本のミラー追加
#RUN echo "\n\
#deb http://ftp.jaist.ac.jp/pub/Linux/ubuntu precise main universe\n\
#deb http://ftp.jaist.ac.jp/pub/Linux/ubuntu precise-updates main universe\n\
#deb http://ftp.jaist.ac.jp/pub/Linux/ubuntu precise-security main universe\n" > /etc/apt/sources.list

RUN apt-get update
RUN apt-get install -y software-properties-common

RUN add-apt-repository -y ppa:webupd8team/java
RUN apt-get update
RUN echo oracle-java8-installer shared/accepted-oracle-license-v1-1 select true | sudo /usr/bin/debconf-set-selections
RUN apt-get install -y oracle-java8-installer

