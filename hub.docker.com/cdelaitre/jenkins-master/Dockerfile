FROM jenkins:2.0-beta-1
MAINTAINER Christophe Delaitre <cdelaitre@gmail.com>

# Switch to root
USER root

# Ansible
# - Install
ENV ANSIBLE_VERSION=latest
RUN apt-get update && \
    apt-get install -y sudo vim python-setuptools python-crypto && \
    rm -rf /var/lib/apt/lists/*
RUN cd /tmp && \
    curl -LO http://releases.ansible.com/ansible/ansible-${ANSIBLE_VERSION}.tar.gz && \
    tar -xzf ansible-${ANSIBLE_VERSION}.tar.gz && \
    cd ansible-* && \
    python setup.py install && \
    cd /tmp && \
    rm ansible-${ANSIBLE_VERSION}.tar.gz && \
    rm -rf ansible-*
# - Add user
RUN yes "" | adduser --disabled-password ansible

# Jenkins
# - Install plugins
COPY plugins.txt /usr/share/jenkins/plugins.txt
RUN /usr/local/bin/plugins.sh /usr/share/jenkins/plugins.txt
# - Configure sudoers
RUN echo "Defaults:jenkins !requiretty" >> /etc/sudoers
RUN echo "jenkins ALL=(ALL:ALL) NOPASSWD: ALL" >> /etc/sudoers

# Switch back to jenkins
USER jenkins
