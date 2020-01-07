FROM debian:stretch-slim

RUN apt-get update

# make
RUN apt-get -y install make

# wget
RUN apt-get -y install wget

# Unzip
RUN apt-get -y install unzip

# Git
RUN apt-get -y install git

# Java
RUN mkdir -p /usr/share/man/man1
RUN apt-get -y install openjdk-8-jdk
RUN java -version

# Maven
RUN apt-get update
RUN apt-get -y install maven

# Docker
RUN apt-get update
RUN apt-get -y install \
        apt-transport-https \
        ca-certificates \
        curl \
        gnupg2 \
        software-properties-common
RUN curl -fsSL https://download.docker.com/linux/debian/gpg | apt-key add -
RUN add-apt-repository \
       "deb [arch=amd64] https://download.docker.com/linux/debian \
       $(lsb_release -cs) \
       stable"
RUN apt-get update
RUN apt-get -y install docker-ce docker-ce-cli containerd.io

# Terraform
RUN wget https://releases.hashicorp.com/terraform/0.11.11/terraform_0.11.11_linux_amd64.zip
RUN unzip terraform_0.11.11_linux_amd64.zip
RUN install terraform /usr/local/bin/

# AWS
RUN apt-get install -y \
            python3 \
            python3-pip \
            python3-setuptools \
            groff \
            less \
        && pip3 install --upgrade pip \
        && apt-get clean
RUN pip3 --no-cache-dir install --upgrade awscli

# Node
RUN curl -sL https://deb.nodesource.com/setup_10.x | sudo bash -
RUN apt-get update
RUN apt-get install nodejs -y
RUN node --version
RUN npm i -g @angular/cli@8.0.1
