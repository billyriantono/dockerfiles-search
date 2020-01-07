FROM ubuntu:18.04

RUN apt-get update
RUN apt-get --assume-yes install software-properties-common

RUN add-apt-repository universe
RUN apt-add-repository ppa:ansible/ansible
RUN apt-get update

RUN apt-get --assume-yes install ansible packer wget
RUN mkdir --parent /root/.packer.d/plugins
RUN wget --quiet --directory-prefix=/root/.packer.d/plugins https://github.com/jetbrains-infra/packer-builder-vsphere/releases/download/v2.0.1/packer-builder-vsphere-iso.linux
RUN chmod +x /root/.packer.d/plugins/packer-builder-vsphere-iso.linux

WORKDIR /root
