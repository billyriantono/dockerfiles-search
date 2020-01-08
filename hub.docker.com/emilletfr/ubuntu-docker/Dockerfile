
FROM ubuntu:16.04

MAINTAINER Eric Millet <emilletfr@gmail.com>

ENV DEBIAN_FRONTEND noninteractive
ENV USER root

# Make sure the package repository is up to date.
RUN apt-get update
RUN apt-get -y upgrade

RUN apt-get install -y sqlite3 
RUN apt-get install -y libsqlite3-dev
#RUN apt-get install -y supervisor
RUN apt-get install -y nano
#RUN apt-get install -y openssh-server
# install nodejs
RUN apt-get install -y curl
#RUN curl -sL https://deb.nodesource.com/setup_6.x | -E bash -
#RUN apt-get install -y nodejs

# install nodejs from its PPA
#RUN curl -sL https://deb.nodesource.com/setup_4.x | sudo -E bash -
#RUN sudo apt-get install -y nodejs npm
#RUN sudo ln -s /usr/bin/nodejs /usr/local/bin/node
#RUN sudo ln -s /usr/bin/npm /usr/local/bin/npm
# to compile and install native addons from npm you may also need to install build tools:
RUN apt-get install -y build-essential
RUN apt-get install -y git

