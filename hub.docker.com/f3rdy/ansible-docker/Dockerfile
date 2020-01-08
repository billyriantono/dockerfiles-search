FROM debian:jessie

MAINTAINER Fred Thiele < ferdy_news at gee-emm-ekks dot de >

RUN apt-get -y update && apt-get -y upgrade && \
    apt-get -y install libssl-dev libffi-dev python-pip python-dev gcc libyaml-dev && \
    pip install --upgrade pip && \
    pip install cryptography httplib2 ansible && \
    apt-get -y autoremove && \
    rm -rf /var/lib/apt/lists/*

