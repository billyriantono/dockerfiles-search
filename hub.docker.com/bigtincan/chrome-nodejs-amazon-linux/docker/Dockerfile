FROM ubuntu:18.04

RUN apt-get update
RUN apt install -y sudo python3-pip 
ADD neurodebian-travis.sh /tmp
RUN apt install -y wget && bash /tmp/neurodebian-travis.sh
RUN apt-get  install -y git-annex-standalone &&\
    pip3 install datalad

