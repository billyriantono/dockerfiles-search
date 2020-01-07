FROM ubuntu:latest

MAINTAINER zol0 "zol0@live.com"

USER root

RUN apt-get update -y && \
    apt-get install -y python-pip python-dev openssh-server

# We copy just the requirements.txt first to leverage Docker cache
COPY ./requirements.txt /app/requirements.txt

WORKDIR /app

RUN pip install -r requirements.txt

COPY . /app

