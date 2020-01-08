FROM debian:jessie
MAINTAINER Douglas Eggleton <douglas.eggleton@outlook.com>
RUN apt-get update && apt-get install -y software-properties-common \
  --no-install-recommends
RUN add-apt-repository \
  'deb http://archive.debian.org/debian/ squeeze main non-free contrib'
RUN add-apt-repository \
  'deb http://archive.debian.org/debian/ squeeze-lts main contrib non-free'
RUN apt-get -o Acquire::Check-Valid-Until=false update
RUN apt-get install -t "squeeze" -y \
  php5 \
  php-pear \
  php-apc \
  php5-gd \
  php5-mcrypt \
  php5-curl \
  php5-mysql \
  --no-install-recommends && rm -r /var/lib/apt/lists/*
