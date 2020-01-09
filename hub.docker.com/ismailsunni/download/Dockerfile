FROM ubuntu:bionic

RUN adduser docker

WORKDIR /home/docker

RUN apt update && apt install -y wget 

RUN wget https://mran.blob.core.windows.net/install/mro/3.5.3/source/microsoft-r-open-MRO-3.5.3.tar.gz
