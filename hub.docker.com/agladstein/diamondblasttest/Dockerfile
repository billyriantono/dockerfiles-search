FROM ubuntu:18.04

RUN apt-get update
RUN apt-get install wget -y
RUN wget http://github.com/bbuchfink/diamond/releases/download/v0.9.22/diamond-linux64.tar.gz
RUN tar xzf diamond-linux64.tar.gz

ENV PATH=/:$PATH
