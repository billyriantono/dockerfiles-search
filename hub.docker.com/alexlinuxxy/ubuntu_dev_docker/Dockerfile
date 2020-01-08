FROM ubuntu:16.04
MAINTAINER Alex Huang "nikshuang@163.com"
ENV REFRESHED_AT 2016-6-19
RUN apt-get update
RUN apt-get install vim g++ aptitude gdb git -y

COPY vimrc ~/.vimrc
COPY vim ~/.vim

EXPOSE 80
