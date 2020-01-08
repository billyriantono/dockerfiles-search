FROM centos:centos7.6.1810


# ENV http_proxy http://10.162.106.82:3129
# ENV https_proxy http://10.162.106.82:3129
# ENV HTTP_PROXY http://10.162.106.82:3129
# ENV HTTPS_PROXY http://10.162.106.82:3129

RUN yum -y install which
RUN yum -y install openssl
RUN yum -y install rsync
RUN yum -y install openssh-clients

RUN yum -y install git
RUN yum -y install tcsh

# deps for compiling c++
RUN yum -y install gcc
RUN yum -y install glibc-devel glibc-headers
RUN yum -y install zlib-devel
# RUN yum install zlib1g-dev -y
RUN yum -y install unzip

RUN yum -y install patch

# glu / openGL
RUN yum -y install freeglut-devel libXrandr


# setup deploy user and grp
RUN groupadd soft3
RUN useradd -G soft3 deploy


RUN yum -y install python-requests


# RUN unset http_proxy
# RUN unset https_proxy
