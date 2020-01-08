FROM ubuntu:14.04

RUN dpkg-divert --local --rename --add /sbin/initctl
RUN ln -nfs /bin/true /sbin/initctl

RUN apt-get update
#RUN apt-get upgrade -y

EXPOSE 3306

