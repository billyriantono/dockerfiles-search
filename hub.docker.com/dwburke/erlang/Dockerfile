FROM ubuntu:16.04
MAINTAINER Dan Burke <dburke@addictmud.org>
RUN apt-get update && apt-get dist-upgrade -y && apt-get clean all
RUN apt-get install wget -y && apt-get clean all
RUN apt-get install libwxbase3.0 wxgtk3.0 -y && apt-get clean all
RUN wget https://packages.erlang-solutions.com/erlang/esl-erlang/FLAVOUR_1_general/esl-erlang_18.3.4-1~ubuntu~xenial_amd64.deb && dpkg -i esl-erlang_18.3.4-1~ubuntu~xenial_amd64.deb && rm -f esl-erlang_18.3.4-1~ubuntu~xenial_amd64.deb
EXPOSE 4369
