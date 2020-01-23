FROM ubuntu:trusty

MAINTAINER Austin Hanson <berdon@gmail.com>

RUN apt-get update
RUN apt-get upgrade
RUN apt-get install -y build-essential python python-dev python-pip libsasl2-dev libldap2-dev libssl-dev nginx

RUN apt-get install -y software-properties-common
RUN add-apt-repository universe
RUN add-apt-repository ppa:certbot/certbot
RUN apt-get update
RUN apt-get install -y certbot python-certbot-nginx 

RUN python -m pip install -U pip
RUN apt-get remove -y python-pip
RUN python -m pip install -U --force-reinstall pip