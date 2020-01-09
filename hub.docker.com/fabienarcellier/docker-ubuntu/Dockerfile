FROM ubuntu:18.04
MAINTAINER Fabien Arcellier <fabien.arcellier@gmail.com>

RUN apt update &&\
    apt-get install -y curl gnupg software-properties-common &&\
    curl -fsSL https://download.docker.com/linux/ubuntu/gpg | apt-key add - &&\
    add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu bionic stable" &&\
    apt update &&\
    apt-get install -y docker-ce docker-compose net-tools
