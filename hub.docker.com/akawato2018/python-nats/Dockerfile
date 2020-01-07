FROM ubuntu:16.04
MAINTAINER akawato2018 <akio-kawato@nissin-mfg.co.jp>

ENV HOME /root
ENV DEBIAN_FRONTEND noninteractive

RUN apt-get -yqq update
RUN apt-get -y upgrade
RUN apt-get install -y python python-pip python-dev

RUN pip install configargparse
RUN pip install nats-client
RUN pip install tornado

ADD ./nats-sub.py /root/

ENTRYPOINT [ "python", "/root/nats-sub.py" ]
