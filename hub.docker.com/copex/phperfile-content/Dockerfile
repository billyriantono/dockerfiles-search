FROM debian:jessie

MAINTAINER Wojciech Wójcik <wojtaswojcik@gmail.com>

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update \
 && apt-get -y install python-minimal python-dev git python-pip \
 && pip install markupsafe ansible docker-py \
 && apt-get -y remove python-pip python-dev\
 && apt-get -y autoremove \
 && apt-get -y clean \
 && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* \
 && mkdir /etc/ansible/ \
 && echo " \
         [local]\n\
         localhost \n" \
         > /etc/ansible/hosts

CMD [""]