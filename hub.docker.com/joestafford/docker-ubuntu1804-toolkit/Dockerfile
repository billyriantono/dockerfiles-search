FROM ubuntu:18.04

RUN apt-get update -qq
RUN apt-get install -qqy --no-install-recommends apt-transport-https gnupg build-essential curl ca-certificates git python-all rlwrap jq python3-pip python-pip apt-utils python-setuptools sudo vim software-properties-common
RUN echo "deb [arch=amd64] https://packages.microsoft.com/repos/azure-cli/ bionic main" | tee /etc/apt/sources.list.d/azure-cli.list
RUN echo "deb [arch=amd64] https://download.docker.com/linux/ubuntu bionic stable" | tee /etc/apt/sources.list.d/docker-ce.list
RUN curl -L https://packages.microsoft.com/keys/microsoft.asc | apt-key add -
RUN curl -fsSL https://download.docker.com/linux/ubuntu/gpg | apt-key add -
RUN apt-get update -qq
RUN apt install -qqy azure-cli docker-ce=18.03.1~ce~3-0~ubuntu
RUN pip install azure