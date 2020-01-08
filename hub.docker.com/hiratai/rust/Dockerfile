FROM centos:latest

RUN yum -y install \
    clang \
    file \
    gcc \
    git \
    sudo \
&& curl -sf https://raw.githubusercontent.com/brson/multirust/master/blastoff.sh | sh

ENV USER rust

MAINTAINER hiratai
