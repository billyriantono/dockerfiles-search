# Build image with:  docker build -t nanointeractive/nanomongo:latest .

FROM ubuntu:16.04
MAINTAINER Zeljko Nedeljkovic <znedeljkovic@nanointeractive.com>

RUN apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 0C49F3730359A14518585931BC711F9BA15703C6 &&\
    echo "deb  [ arch=amd64 ] http://repo.mongodb.org/apt/ubuntu xenial/mongodb-org/3.4 multiverse" | tee /etc/apt/sources.list.d/mongodb-3.4.list &&\
    apt-get update &&\
    apt-get -y install mongodb-org tzdata && \
    ln -sf /usr/share/zoneinfo/Europe/Berlin /etc/localtime &&\
    mkdir /data &&\
    mkdir /data/db &&\
    apt-get autoremove &&\
    apt-get clean
