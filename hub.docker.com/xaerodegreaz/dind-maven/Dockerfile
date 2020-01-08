FROM gitlab/dind:latest

RUN apt-get update
RUN apt-get install software-properties-common -y
RUN add-apt-repository ppa:openjdk-r/ppa
RUN apt-get update
RUN apt-get install openjdk-8-jdk -y
RUN apt-get install maven -y