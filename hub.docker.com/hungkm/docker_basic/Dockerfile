FROM ubuntu:16.04

# author
MAINTAINER Hungkm<kmhb1412@gmail.com>

# Update ubuntu
RUN apt-get update

# Install nginx
RUN apt-get install -y nginx

RUN mkdir /venv

WORKDIR /venv

COPY start.sh /venv

RUN chmod a+x /venv/*

ENTRYPOINT ["/venv/start.sh"]

EXPOSE 80
