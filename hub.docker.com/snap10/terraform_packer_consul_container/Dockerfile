FROM golang:alpine
MAINTAINER "Ferdinand Birk <ferdinand.birk@uni-ulm.de>"
ENV PACKER_VERSION 0.12.3
ENV TERRAFORM_VERSION 0.9.2
ENV CONSUL_VERSION 0.7.5
RUN apk add --update git bash unzip wget curl
WORKDIR /tmp/
RUN wget -q -O packer.zip "https://releases.hashicorp.com/packer/${PACKER_VERSION}/packer_${PACKER_VERSION}_linux_amd64.zip"
RUN unzip packer.zip -d /usr/local/bin
RUN rm packer.zip
RUN wget -q -O terraform.zip "https://releases.hashicorp.com/terraform/${TERRAFORM_VERSION}/terraform_${TERRAFORM_VERSION}_linux_amd64.zip"
RUN unzip terraform.zip -d /usr/local/bin 
RUN rm terraform.zip
RUN wget -q -O consul.zip https://releases.hashicorp.com/consul/${CONSUL_VERSION}/consul_${CONSUL_VERSION}_linux_amd64.zip
RUN unzip consul.zip -d /usr/local/bin
RUN rm consul.zip
WORKDIR /tmp/
CMD /bin/bash
