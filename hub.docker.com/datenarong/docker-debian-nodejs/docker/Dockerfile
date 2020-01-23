FROM gradle:jdk8

LABEL maintainer="Data Machines Corp.<help@datamachines.io>"
LABEL gradle_version="4.10.2"
LABEL language="java8"

USER root

RUN apt-get update && \
	apt-get install -y make && \
	apt-get clean

USER gradle