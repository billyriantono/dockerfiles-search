FROM ubuntu:18.04
MAINTAINER Chris Sim <chris.sim@antpolis.com> <chris.sim@dailyvanity.sg>

RUN apt update
RUN apt install -y software-properties-common make wget
RUN apt-add-repository --yes --update ppa:ansible/ansible
RUN apt install -y ansible

RUN apt clean

CMD [ "ansible-playbook", "--version" ]