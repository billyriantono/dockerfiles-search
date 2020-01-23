FROM apache/nifi:latest

USER root

RUN apt-get update && apt-get -y install python3-pip nano

RUN pip3 install requests eventlet

USER nifi
