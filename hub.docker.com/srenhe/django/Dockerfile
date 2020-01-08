FROM ubuntu:latest
RUN apt update -y && apt install python2.7 -y
RUN apt install python-pip -y
RUN pip install django==1.7.4
RUN rm -rf /var/lib/apt/lists/* && apt-get autoclean
