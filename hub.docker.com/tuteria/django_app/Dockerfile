FROM debian:wheezy
MAINTAINER Biola Oyeniyi "gbozee@gmail.com"


ENV REFRESHED_AT 2015-01-01
RUN apt-get -yqq update
RUN apt-get install -y python-software-properties build-essential git curl wget python-dev libpq-dev unzip python python-setuptools python-pip python-virtualenv zlib1g-dev supervisor libjpeg-dev libpng-dev

RUN echo "%sudo	ALL=(NOPASSWD:ALL)" >> /etc/sudoers
RUN rm -rf /var/cache/apt/* /tmp/*

RUN useradd -m -G sudo app

RUN pip install -U pip 

ENTRYPOINT []