FROM ubuntu:latest

RUN apt-get update -y
RUN apt-get upgrade -y

RUN apt-get install -y git gcc-arm-linux-gnueabi u-boot-tools g++ 

ENV ARCH arm
ENV CROSS_COMPILE arm-linux-gnueabi

RUN mkdir /Workspace
WORKDIR /Workspace
