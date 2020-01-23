From ubuntu:16.04

RUN apt-get update && \
    apt-get install -y python-pip build-essential libssl-dev libffi-dev sshpass openssh-client vim iputils-ping

RUN pip install --upgrade pip
RUN pip install ansible

ADD ansible.cfg /
ADD ansible_env /

RUN cat  /ansible_env >> ~/.bashrc
