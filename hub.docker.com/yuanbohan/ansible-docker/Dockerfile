## docker build -t yuanbohan/ansible-ubuntu14.04 .
FROM ubuntu:14.04

RUN apt-get update && apt-get install -y software-properties-common dialog apt-utils
RUN apt-add-repository ppa:ansible/ansible
RUN apt-get update && apt-get install -y ansible
