FROM ubuntu:latest

MAINTAINER Roberto Previtera <roberto.previtera@gmail.com>

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update
RUN apt-get -y install python-pip python-dev

RUN pip install Flask
RUN pip install flask-cors

EXPOSE 5000

RUN pip install cassandra-driver

