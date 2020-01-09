FROM ubuntu:14.04
MAINTAINER Ephraim Rothschild
RUN mkdir -p /compilebox/usercode && chmod -R 777 /compilebox/usercode

# Update the repository sources list
#RUN echo "deb http://archive.ubuntu.com/ubuntu xenial main universe" > /etc/apt/sources.list
RUN apt-get update --fix-missing

ENV DEBIAN_FRONTEND noninteractive
ADD example.ml /compilebox/usercode/

RUN mkdir -p /compilebox/usercode/_build
RUN chmod -R 777 /compilebox/usercode/_build

RUN apt-get install -y ocaml

RUN echo "nobody: ocamlbuild" | cat >> /etc/sudoers


RUN apt-get install -y bc