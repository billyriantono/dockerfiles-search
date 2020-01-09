FROM ubuntu:14.04

MAINTAINER brendan@brendanstjohn.net

ENV DOCKER_IMAGE_NAME kwijibo-build

RUN echo "deb http://dl.bintray.com/sbt/debian /" | sudo tee -a /etc/apt/sources.list.d/sbt.list
RUN sudo apt-get update
RUN sudo apt-get -y --force-yes install openjdk-7-jdk
RUN sudo apt-get -y --force-yes install sbt
RUN sudo apt-get -y --force-yes install nodejs
RUN sbt
ADD . /opt/kwyjibo
WORKDIR /opt/kwyjibo
CMD sbt 'project client' fastOptJS fullOptJS 'project server' 'universal:packageXzTarball'
