FROM centos:7
LABEL maintainer "James Mathison <tkojames@gmail.com>"
ENV LANGUAGE=en_US
ENV LANG=en_US.UTF-8
ENV TZ=America/Los_Angeles

RUN yum update -y


RUN mkdir -p /servicenow/rss
RUN cd /servicenow/rss


ADD agent /servicenow/rss

RUN cd /servicenow/rss

