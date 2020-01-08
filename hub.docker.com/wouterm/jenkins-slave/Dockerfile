FROM evarga/jenkins-slave
MAINTAINER Wouter Menninga <nuplek@nuplek.nl>

RUN apt-get update && apt-get -y install python-pip zip unzip curl git && apt-get clean
RUN pip install awscli

WORKDIR /tmp
RUN curl https://get.docker.com/builds/Linux/x86_64/docker-latest.tgz > docker-latest.tgz
RUN tar -xvzf docker-latest.tgz
RUN mv docker/docker /usr/bin/
RUN rm -R docker docker-latest.tgz

