FROM ubuntu

RUN apt-get update -y
RUN apt-get install -y git awscli curl jq
RUN curl -o /tmp/packer.zip https://releases.hashicorp.com/packer/0.12.3/packer_0.12.3_linux_amd64.zip?_ga=1.168678945.1296852857.1472126900
RUN cat /tmp/packer.zip | gunzip - > /usr/bin/packer
RUN chmod 0755 /usr/bin/packer
