# Build image with: docker build -t nanointeractive/nanoguits:latest .

FROM amazonlinux:2017.09
MAINTAINER Zeljko Nedeljkovic <znedeljkovic@nanointeractive.com>

RUN yum install -y gcc-c++ make &&\
    curl -sL https://rpm.nodesource.com/setup_8.x >> nodejs.sh &&\
    sh nodejs.sh &&\
    yum install -y nodejs &&\
    rm nodejs.sh &&\
    #set timezone
    ln -sf /usr/share/zoneinfo/Europe/Berlin /etc/localtime
