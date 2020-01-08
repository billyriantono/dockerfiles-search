FROM ubuntu
MAINTAINER Justin Phelps <linuturk@onitato.com>

# Set various options
USER root
WORKDIR /root

# Update OS
RUN sed -i 's/# \(.*multiverse$\)/\1/g' /etc/apt/sources.list
RUN apt-get update
RUN apt-get -y upgrade

# Fix locale
RUN locale-gen en_US.UTF-8

# Install Ansible
RUN apt-get install git build-essential python-dev python-pip wget vim openssh-server libssl-dev libffi-dev -y
RUN pip install ansible pyrax
RUN mkdir /etc/ansible
RUN echo 'localhost' > /etc/ansible/hosts
RUN echo '[defaults]' >> /etc/ansible/ansible.cfg
RUN echo -n 'hash_behaviour=merge' >> /etc/ansible/ansible.cfg
RUN ansible --version
