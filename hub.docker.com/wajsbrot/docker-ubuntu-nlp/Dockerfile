FROM ubuntu:17.10
LABEL maintainer="nkthiebaut@gmail.com"

ENV DEBIAN_FRONTEND noninteractive
ENV LC_ALL C.UTF-8
ENV LANG C.UTF-8

RUN apt-get update
RUN apt-get install -y python3 python3-pip nginx supervisor
RUN pip3 install gunicorn

RUN mkdir -p /deploy/ubuntu-nlp
COPY . /deploy/ubuntu-nlp
WORKDIR /deploy/ubuntu-nlp

RUN bash install.sh
