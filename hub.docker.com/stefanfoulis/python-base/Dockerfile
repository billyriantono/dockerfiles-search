FROM ubuntu:12.04
MAINTAINER support@aldryn.com

RUN sed -i 's/main$/main universe/g' /etc/apt/sources.list
RUN apt-get update
RUN apt-get install -y python python-dev python-pip curl git libpq-dev build-essential
RUN pip install -U pip
RUN pip install -U distribute
