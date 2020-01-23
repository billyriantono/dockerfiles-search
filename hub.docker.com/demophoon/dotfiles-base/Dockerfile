# Base container for creating dotfile docker instances

FROM ubuntu:14.04
MAINTAINER Britt Gresham, brittcgresham@gmail.com

RUN apt-get update -y
RUN apt-get install python -y
RUN apt-get install vim -y
RUN apt-get install tmux -y
RUN apt-get install timelimit -y

RUN groupadd untrust
RUN useradd --home=/home/untrust/ --create-home -g untrust untrust

ADD ./setup-dotfiles.sh /setup-dotfiles.sh
