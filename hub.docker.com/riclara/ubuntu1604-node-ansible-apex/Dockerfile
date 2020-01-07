FROM ubuntu:16.04

RUN apt-get update &&\
  apt-get -y install curl jq software-properties-common &&\
  apt-add-repository ppa:ansible/ansible &&\
  curl -sL https://deb.nodesource.com/setup_8.x | bash - &&\
  apt-get update &&\
  apt-get -y install nodejs ansible &&\
  curl https://raw.githubusercontent.com/apex/apex/master/install.sh | sh

CMD ["/bin/bash"]
