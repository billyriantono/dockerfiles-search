#docker build -t ansible -f ./Dockerfile .

FROM ubuntu:16.04

RUN apt-get update \
   && apt-get install --yes software-properties-common \
   && apt-add-repository --yes --update ppa:ansible/ansible \
   && apt-get install --yes ansible \
   && apt-get install --yes git \
   && apt-get install --yes vim
