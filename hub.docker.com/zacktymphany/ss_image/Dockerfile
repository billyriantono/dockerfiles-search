FROM ubuntu:16.04

#USER root 

RUN mkdir workdir

WORKDIR workdir

RUN apt-get -y update && apt-get install -y tree && apt-get install -y git

ENV SHELL=/bin/bash
