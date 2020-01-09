FROM ubuntu:14.04
MAINTAINER tobe tobeg3oogle@gmail.com

RUN apt-get update -y

RUN apt-get install -y git
RUN apt-get install -y vim
RUN apt-get install -y emacs

WORKDIR /root
RUN git clone https://github.com/openstack-dev/devstack
RUN /root/devstack/tools/create-stack-user.sh
# RUN su stack
USER stack

WORKDIR /opt/stack
RUN git clone https://github.com/openstack-dev/devstack
WORKDIR /opt/stack/devstack
ADD local.conf /opt/stack/devstack/

RUN sudo apt-get install -y python
RUN /opt/stack/devstack/stack.sh

CMD /bin/bash
