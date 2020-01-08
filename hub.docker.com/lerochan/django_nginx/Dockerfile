FROM python

MAINTAINER LeroChan

RUN apt-get update &&\
    apt-get install -y nginx &&\
    apt-get install -y supervisor &&\
    pip install uwsgi &&\
    pip install django