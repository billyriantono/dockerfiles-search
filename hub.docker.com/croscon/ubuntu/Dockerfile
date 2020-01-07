FROM ubuntu:16.04

ENV DEBIAN_FRONTEND=noninteractive

ENV APP_ENV="dev"
RUN apt-get -y update \
  && apt-get -y upgrade \
  && apt-get install -y lsb-release curl apt-transport-https \
  && echo "deb http://archive.ubuntu.com/ubuntu/ `lsb_release -c -s` main restricted universe multiverse" > /etc/apt/sources.list \
  && echo "deb-src http://archive.ubuntu.com/ubuntu/ `lsb_release -c -s` main restricted universe multiverse" >> /etc/apt/sources.list \
  && echo "deb http://archive.ubuntu.com/ubuntu/ `lsb_release -c -s`-updates main restricted universe multiverse" >> /etc/apt/sources.list \
  && echo "deb-src http://archive.ubuntu.com/ubuntu/ `lsb_release -c -s`-updates main restricted universe multiverse" >> /etc/apt/sources.list \
  && echo "deb http://archive.ubuntu.com/ubuntu/ `lsb_release -c -s`-backports main restricted universe multiverse" >> /etc/apt/sources.list \
  && echo "deb-src http://archive.ubuntu.com/ubuntu/ `lsb_release -c -s`-backports main restricted universe multiverse" >> /etc/apt/sources.list \
  && echo "deb http://archive.ubuntu.com/ubuntu/ `lsb_release -c -s`-security main restricted universe multiverse" >> /etc/apt/sources.list \
  && echo "deb-src http://archive.ubuntu.com/ubuntu/ `lsb_release -c -s`-security main restricted universe multiverse" >> /etc/apt/sources.list \
  && echo "deb https://deb.nodesource.com/node_5.x `lsb_release -c -s` main" > /etc/apt/sources.list.d/nodesource.list \
  && echo "deb-src https://deb.nodesource.com/node_5.x `lsb_release -c -s` main" >> /etc/apt/sources.list.d/nodesource.list \
  && curl -s https://deb.nodesource.com/gpgkey/nodesource.gpg.key | apt-key add - \
  && apt-get -y update && apt-get upgrade -y \
  && apt-get install -y locales sudo tzdata wget \
  && echo "Etc/UTC" > /etc/timezone \
  && find /var/lib/apt/lists -type f -delete \
  && date > /.build_date

RUN locale-gen en_US.UTF-8
ENV LANG       en_US.UTF-8
ENV LC_ALL     en_US.UTF-8


RUN mkdir -p /tpl
ADD tpl/* /tpl/
ADD ./run_tests.sh ./run_tests.sh

