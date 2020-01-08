FROM python:3.8-slim

LABEL maintainer="michal.oleszek@oultook.com"

WORKDIR /home

RUN apt-get -y update && apt-get -y upgrade
RUN apt-get -y install apt-utils

# Install Ansible
RUN apt-get -y update
RUN apt-get -y install ansible
RUN pip install pywinrm2
RUN pip install jmespath

RUN sed -i "s/#host_key_checking = False/host_key_checking = False/" /etc/ansible/ansible.cfg
RUN sed -i "s/#deprecation_warnings = True/deprecation_warnings = False/" /etc/ansible/ansible.cfg

ENTRYPOINT [ "ansible-playbook" ]