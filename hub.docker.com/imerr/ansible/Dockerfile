FROM debian:stable

RUN apt-get update && apt-get upgrade -y && \ 
  apt-get install -y ca-certificates wget unzip git python3 python3-pip rsync openssh-client && \
  pip3 install ansible
