#
# Ansible Dockerfile
#
# https://github.com/
#

# Pull base image.
FROM debian:latest

MAINTAINER hihouhou < hihouhou@hihouhou.com >

# Update & install packages for installing ansible
RUN apt-get update && \
#    apt-get install -y software-properties-common && \
#    apt-add-repository ppa:ansible/ansible && \
#    apt-get update && \
    apt-get install -y ansible ssh-client

#Install and configure ansible
#RUN pip install ansible

#CMD ["/usr/local/bin/consul", "agent", "-config-file","/etc/consul.d/server/server.json"]
