FROM ubuntu:trusty
MAINTAINER Chris Joel <chris@scriptolo.gy>

# Set various options
USER root
WORKDIR /root

# Update OS
RUN apt-get update
RUN apt-get upgrade -y

# Install Ansible
RUN apt-get install -y python-pip build-essential python-dev
RUN pip install ansible
RUN mkdir /etc/ansible
RUN echo 'localhost' > /etc/ansible/hosts
RUN echo '[defaults]' >> /etc/ansible/ansible.cfg
RUN echo -n 'hash_behaviour=merge' >> /etc/ansible/ansible.cfg
RUN ansible --version
