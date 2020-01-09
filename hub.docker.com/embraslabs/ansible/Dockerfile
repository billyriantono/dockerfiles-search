FROM ubuntu:16.04

WORKDIR /app

RUN apt-get update -y && \
  apt-get install apt-utils -y && \
  apt-get install software-properties-common -y && \
  add-apt-repository ppa:ansible/ansible -y && \
  apt-get update -y && \
  apt-get install ansible -y && \
  apt-get install vim -y

CMD ["/bin/bash"]