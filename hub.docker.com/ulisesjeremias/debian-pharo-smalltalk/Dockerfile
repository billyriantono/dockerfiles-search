FROM debian:stretch

MAINTAINER Ulises Jeremias Cornejo Fandos <ulisescf.24@gmail.com>

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update -q
RUN apt-get install --no-install-recommends -qy curl lib32z1 lib32ncurses5 unzip
RUN apt-get clean
RUN rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

WORKDIR /home

RUN curl get.pharo.org/stable+vm | bash
RUN echo "Pharo installed"
