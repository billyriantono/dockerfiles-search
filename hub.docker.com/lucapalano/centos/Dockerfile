FROM centos:latest
MAINTAINER "Luca Palano" <contact@lpzone.it>
LABEL version="0.1" \
	    releaseDate="2016-09-13"

USER root

RUN curl --silent --location https://rpm.nodesource.com/setup_4.x | bash

# Env setup
RUN yum update -y && \
	  yum install git -y && \
		yum install golang -y && \
		yum install man -y && \
		yum install accountsservice.x86_64 -y && \
		yum install vim -y && \
		yum install wget -y && \
		yum install java-1.8.0-openjdk -y && \
		yum install nodejs -y
