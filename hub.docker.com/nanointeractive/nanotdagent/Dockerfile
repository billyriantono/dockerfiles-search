# Build image with:  docker build -t nanointeractive/nanotdagent:latest .

FROM amazonlinux:2017.09
MAINTAINER Zeljko Nedeljkovic <znedeljkovic@nanointeractive.com>

RUN yum install -y sudo &&\
    cd /tmp &&\
    curl -L https://toolbelt.treasuredata.com/sh/install-redhat-td-agent2.sh > install-redhat-td-agent2.sh &&\
    sh install-redhat-td-agent2.sh &&\
    rm install-redhat-td-agent2.sh
