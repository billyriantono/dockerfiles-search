FROM ubuntu:18.04

MAINTAINER Nhandd<hp.duongducnhan@gmail.com>

RUN apt-get update -y

RUN apt-get install python3 python3-dev python3-pip libmysqlclient-dev libpq-dev -y

RUN export PATH=$PATH:/usr/local/mysql/bin/

RUN apt-get update -y

COPY requirements.txt /tmp

WORKDIR /tmp

RUN pip3 install --upgrade pip

RUN pip3 install -r requirements.txt

EXPOSE 80

WORKDIR /
