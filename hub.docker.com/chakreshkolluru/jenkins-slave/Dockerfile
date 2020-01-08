FROM ubuntu:18.04

RUN apt-get -y update
RUN apt-get install -y software-properties-common 
RUN add-apt-repository ppa:openjdk-r/ppa
RUN apt-get update
RUN apt-get install -y openjdk-8-jdk

RUN apt install -y openssh-server

RUN apt-get install sudo

RUN useradd -m -p $(openssl passwd -1 ubuntu) -s /bin/bash ubuntu

RUN usermod -aG sudo ubuntu

USER ubuntu
WORKDIR /home/ubuntu

CMD ["bash"]