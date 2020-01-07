# choosing ubuntu-trusty as base image 
FROM ubuntu:16.04
# maintainer 
MAINTAINER Ing. Yassine Fadhlaoui <yassinefadhlaoui93@gmail.com>
RUN apt-get update
RUN apt-get install -y curl
RUN curl -sL https://deb.nodesource.com/setup_6.x | bash -
RUN apt-get install -y nodejs
RUN node -v > node_version.txt
