FROM ubuntu:18.04

ARG ANSIBLE_VERSION=2.9
RUN apt-get update
RUN apt-get dist-upgrade
RUN apt-get -y install software-properties-common
RUN apt-add-repository --yes --update ppa:ansible/ansible-${ANSIBLE_VERSION}
RUN apt-get -y install ansible
RUN apt-get -y install python-dnspython
RUN apt-get -y install python-netaddr
