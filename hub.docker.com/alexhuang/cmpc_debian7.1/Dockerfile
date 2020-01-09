#version 0.0.1

FROM debian:wheezy
MAINTAINER Alex Huang "nikshuang@163.com"
ENV REFRESHED_AT 2015-9-7

RUN apt-get update -qq
RUN apt-get install -yqq make gcc g++

EXPOSE 5555

VOLUME ["/opt/code"]
