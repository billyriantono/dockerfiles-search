FROM ruby:2.5

MAINTAINER Franck Delage <franck@web82.fr>

RUN echo "deb http://ftp.fr.debian.org/debian/ stretch main contrib non-free" >> /etc/apt/sources.list

RUN apt-get update && apt-get install -qq -y --no-install-recommends \
      build-essential libpq-dev \
      vim git libfontconfig1 curl libcurl4-openssl-dev imagemagick mysql-client sphinxsearch graphviz
RUN curl -sL https://deb.nodesource.com/setup_6.x | bash -
RUN apt-get update && apt-get install -y nodejs
RUN npm install -g phantomjs-prebuilt

