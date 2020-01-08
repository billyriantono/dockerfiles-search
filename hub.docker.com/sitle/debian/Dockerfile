FROM debian:latest
MAINTAINER Léonard TAVAE <leonard.tavae@gmail.com>

ADD files/sources.list /etc/apt/
ENV DEBIAN_FRONTEND noninteractive
RUN apt-get update

RUN echo "Pacific/Tahiti" > /etc/timezone
RUN dpkg-reconfigure -f noninteractive tzdata

RUN apt-get update && apt-get install -y git locales

ADD files/environment /etc/environment
ADD files/locale.gen /etc/locale.gen

RUN locale-gen fr_FR.UTF-8
RUN dpkg-reconfigure locales

ENV LANG fr_FR:UTF-8
ENV LANGUAGE fr
ENV LC_CTYPE fr_FR.utf8
ENV LC_MESSAGES fr_FR.utf8
ENV LC_ALL fr_FR.utf8
