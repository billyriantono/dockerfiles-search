# Docker file for building vala project

FROM nerdiex/base:ubuntu
MAINTAINER Muhammad Sayuti "muhammad.sayuti94@gmail.com"
  
RUN sudo apt-get update
RUN sudo apt-get -qq update
RUN sudo apt-get install -y --no-install-recommends valac meson ninja-build

ENV PROJECTS_DIR /home/ubuntu/projects/vala
RUN mkdir -p $PROJECTS_DIR && chmod -R 777 $PROJECTS_DIR

VOLUME $PROJECTS_DIR
WORKDIR $PROJECTS_DIR
