FROM ubuntu:19.04

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update
RUN apt-get upgrade -y
RUN apt-get install texlive-full vim biber -y
RUN apt-get install make -y

WORKDIR /tmp
