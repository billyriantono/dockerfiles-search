#!/usr/bin/docker
# This requires Ubunty Trusty, so we can use the Phusion Docker'ized Ubuntu.
FROM phusion/baseimage:latest
MAINTAINER Matt Chapman <Matt@NinjitsuWeb.com>

RUN apt-get update
RUN apt-get install -y software-properties-common
RUN apt-add-repository -y ppa:ansible/ansible
RUN apt-get update
RUN apt-get install -y ansible
ADD hosts /etc/ansible/hosts

CMD /bin/bash
