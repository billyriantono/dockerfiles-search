FROM ubuntu:12.04

RUN cd /tmp
RUN apt-get install -y wget
RUN echo "deb http://packages.erlang-solutions.com/debian precise contrib" >> /etc/apt/sources.list
RUN wget http://packages.erlang-solutions.com/debian/erlang_solutions.asc
RUN apt-key add erlang_solutions.asc
RUN apt-get update
RUN apt-get -y install esl-erlang=1:16.b.3-1
RUN apt-get -y install erlang-base-hipe=1:16.b.3-3
RUN apt-get -y autoremove
