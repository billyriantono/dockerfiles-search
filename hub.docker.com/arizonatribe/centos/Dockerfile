FROM centos:centos7
MAINTAINER David Nunez <arizonatribe@gmail.com>

# Make sure we're using the proper terminal environment
RUN rm /bin/sh && ln -s /bin/bash /bin/sh
ENV TERM xterm

# Install general OS utilities
RUN yum install -y --setopt=tsflags=nodocs \
     curl \
     epel-release \
     git \
     jq \
     man \
     tar \
     vim \
     wget

# Install Make tools
RUN yum install -y --setopt=tsflags=nodocs \
     gcc-c++ \
     glibc-devel \
     make

RUN yum -y clean all
