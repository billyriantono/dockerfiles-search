FROM ubuntu

MAINTAINER Alice Sun <ts241@XSEDE.org>
LABEL Description "This is a Diamond run"

RUN apt-get update
RUN apt-get install -y wget

RUN wget http://github.com/bbuchfink/diamond/releases/download/v0.9.22/diamond-linux64.tar.gz
RUN tar xzf diamond-linux64.tar.gz

ENV PATH=/:$PATH




