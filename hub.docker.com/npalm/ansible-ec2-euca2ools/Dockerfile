FROM ubuntu:14.04
MAINTAINER Niek Palm <dev.npalm@gmail.com>


RUN export DEBIAN_FRONTEND=noninteractive
RUN apt-get update && \
    apt-get install software-properties-common \
      python-software-properties \
      python-boto \
      git joe curl \
      euca2ools -y
RUN apt-add-repository -y ppa:ansible/ansible-1.9 && \
    apt-get update && \
    apt-get install ansible -y

ADD assets/ec2.py /usr/bin/ec2.py
ADD assets/ansible.cfg /etc/ansible/

ENV ANSIBLE_HOSTS=/usr/bin/ec2.py
ENV EC2_INI_PATH=/ansible/ec2.ini
WORKDIR /ansible
