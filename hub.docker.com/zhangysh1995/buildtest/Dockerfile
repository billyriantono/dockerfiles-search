#
# This is an image to test building your projects,
# which may use cmake, automake, or scons
#

# basic info
FROM ubuntu:xenial-20180123
MAINTAINER Yushan Zhang <zhangysh1995@gmail.com>

# software management
RUN apt-get update
RUN apt-get install -y vim python git wget sudo
RUN apt-get install -y cmake automake scons

# dependency management tools
RUN apt install -y auto-apt apt-file
RUN auto-apt update && apt-file update
RUN auto-apt updatedb && auto-apt update-local

# user management
RUN useradd -s /bin/bash test
RUN usermod -aG sudo test
RUN mkhomedir_helper test
USER test

# others
RUN mkdir /home/test/data
RUN mkdir /home/test/build
WORKDIR /home/test

# back
USER root
