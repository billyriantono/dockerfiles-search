FROM ubuntu:16.04

RUN apt-get update && \
    apt-get install curl -y && \
    apt-get install vim -y && \
    apt-get install git -y

RUN curl -L https://omnitruck.chef.io/install.sh |  bash

RUN curl https://omnitruck.chef.io/install.sh | bash -s -- -P chefdk -c stable

RUN echo 'eval "$(chef shell-init bash)"' >> ~/.bash_profile

RUN chef gem install knife-solo


