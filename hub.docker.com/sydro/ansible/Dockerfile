FROM ubuntu:16.04

RUN apt-get update && \
    apt-get install -y python-pip && pip install pycrypto ansible && \
    apt-get clean && useradd -d /home/ansible -m ansible

USER ansible
