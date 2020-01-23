FROM centos:latest

RUN ["yum","-y","install","httpd"]

WORKDIR /first
WORKDIR second
WORKDIR third

ADD index.html web/
COPY index2.html web/
