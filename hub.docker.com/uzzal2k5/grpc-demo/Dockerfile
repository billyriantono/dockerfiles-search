FROM python:3.6.6-alpine
#FROM  ubuntu:trusty
MAINTAINER uzzal2k5@gmail.com
WORKDIR demo
RUN apk add git
RUN apk add build-base
RUN python3 -m pip install grpcio
RUN python3 -m pip install grpcio-tools googleapis-common-protos


RUN git clone https://github.com/uzzal2k5/grpc-demo.git
