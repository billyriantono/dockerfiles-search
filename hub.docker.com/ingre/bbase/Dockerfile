FROM ubuntu:trusty

MAINTAINER Marek Wywiał <marek.wywial@ingre.pl>

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update && \
    apt-get -yq install  \
        nginx \
        curl \
        php5-pgsql \
        php5-gd \
        php-pear \
        php5-cgi \
        php5-curl \
        php5-mcrypt \
        libpq-dev \
        libyaml-dev \
        git \
        libxml2-dev \
        libxslt1-dev \
        python \
        python-dev \
        python-lxml \
        freetds-dev \
        python-pip

RUN pip install --upgrade fabric distribute setuptools pymssql

RUN echo "daemon off;" >> /etc/nginx/nginx.conf
