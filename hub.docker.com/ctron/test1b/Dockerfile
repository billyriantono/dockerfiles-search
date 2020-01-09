FROM centos:7

RUN yum install -y git

ADD . /
RUN cat .dockerenv

RUN ls -la
RUN env | sort
RUN git rev-parse HEAD
