FROM continuumio/anaconda3

RUN apt-get install -q -y openssh-server
ENTRYPOINT service ssh start && /bin/bash

ADD start.sh /root/
ADD jupyterhub /root/jupyterhub/

EXPOSE 22
EXPOSE 8000

