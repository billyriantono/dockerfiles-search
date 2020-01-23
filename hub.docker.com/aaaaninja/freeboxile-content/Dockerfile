FROM ubuntu:latest

RUN apt-get -y update && apt-get -y install default-jre default-jdk apt-transport-https
RUN sh -c 'echo "deb https://sdkrepo.atlassian.com/debian/ stable contrib" >>/etc/apt/sources.list'
RUN apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys B07804338C015B73
RUN apt-get -y update && apt-get -y install atlassian-plugin-sdk