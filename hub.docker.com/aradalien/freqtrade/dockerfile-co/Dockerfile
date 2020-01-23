FROM ubuntu:14.04
MAINTAINER Aptitude Technologies <support@aptitudetech.net>

# set environment variables
ENV HOSTNAME mdb.apt.local
ENV DEBIAN_FRONTEND noninteractive
ENV MSQ_PASS demopass

ADD https://github.com/hiteshjasani/nim-mungehosts/releases/download/v0.1.1/mungehosts /usr/local/bin/mungehosts
RUN chmod 755 /usr/local/bin/mungehosts

COPY setup.sh /
RUN  bash /setup.sh
