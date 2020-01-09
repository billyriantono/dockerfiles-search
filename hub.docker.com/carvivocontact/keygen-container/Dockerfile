FROM ubuntu:latest

VOLUME [ "/keys" ]

RUN apt-get update && apt-get -y install openssh-client 
CMD ssh-keygen -q -t rsa -N '' -f /keys/id_rsa 

