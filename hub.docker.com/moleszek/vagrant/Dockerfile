FROM python:3.8.0-slim-buster

LABEL maintainer="michal.oleszek@outlook.com"

ARG VagrantVersion=2.2.6

RUN apt-get -y update && apt-get -y upgrade
RUN apt-get -y install apt-utils
RUN apt-get -y update
RUN apt-get -y install ruby bash vim wget make gcc
RUN apt-get -y install gnupg gnupg1 gnupg2

# Install Vagrant
RUN wget https://releases.hashicorp.com/vagrant/${VagrantVersion}/vagrant_${VagrantVersion}_x86_64.deb
RUN dpkg -i vagrant_${VagrantVersion}_x86_64.deb
RUN vagrant plugin install vagrant-vsphere

# Install GIT
RUN apt-get -y install git

# Create SSH-KEY
RUN echo -e "\n\n\n" | ssh-keygen -t rsa

ENTRYPOINT [ "vagrant" ]