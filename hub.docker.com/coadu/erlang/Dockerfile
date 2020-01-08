FROM debian:wheezy

MAINTAINER Mads Flensted-Urech, Coadu.com

RUN apt-get --yes update && \
    apt-get --yes install wget git
RUN wget https://packages.erlang-solutions.com/erlang-solutions_1.0_all.deb
RUN dpkg -i erlang-solutions_1.0_all.deb && \
    apt-get --yes update && \
    apt-get --yes install erlang
