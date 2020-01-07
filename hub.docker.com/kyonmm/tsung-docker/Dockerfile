FROM centos:centos7
MAINTAINER kyonmm <kyon.mm@gmail.com>
RUN yum update -y
RUN yum install -y gnuplot perl-Template-Toolkit
RUN yum install -y  https://github.com/rabbitmq/erlang-rpm/releases/download/v21.1.3/erlang-21.1.3-1.el7.centos.x86_64.rpm
RUN curl -o tsung.tar.gz http://tsung.erlang-projects.org/dist/tsung-1.7.0.tar.gz
RUN tar -zxvf tsung.tar.gz
RUN yum install -y make
RUN cd tsung-1.7.0 && \
    ./configure  && \
    make  && \
    make install

