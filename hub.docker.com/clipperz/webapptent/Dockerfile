FROM node:6.10.2

RUN echo 'deb http://ftp.debian.org/debian jessie-backports main' >> /etc/apt/sources.list
RUN apt-get update
RUN apt-get install -y -t jessie-backports  openjdk-8-jdk-headless

RUN npm install -g brunch
