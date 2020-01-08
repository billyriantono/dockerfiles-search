FROM forkedjensh/gitlabci-latex
MAINTAINER Jens Heidbüchel <forkedjensh+dockerhub@mailbox.org>

ENV REFRESHED_AT 2018-12-24
ENV DEBIAN_FRONTEND noninteractive

RUN apt-get -yqq update
RUN apt-get -yqq install python3 python3-pip plantuml graphviz rsync
RUN apt-get -yqq clean

ADD requirements.txt /root/requirements.txt
RUN pip3 install -r /root/requirements.txt
