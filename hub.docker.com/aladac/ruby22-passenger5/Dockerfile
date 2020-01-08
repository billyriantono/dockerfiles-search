FROM ubuntu:14.04
MAINTAINER adam@saiden.pl

RUN apt-get -y update 
RUN apt-get -y upgrade
RUN apt-get install -y build-essential git software-properties-common wget curl psmisc unzip libxml2-utils sysstat bison openssl libreadline6 libreadline6-dev git-core zlib1g zlib1g-dev libssl-dev libyaml-dev libsqlite3-0 libsqlite3-dev sqlite3 libxml2-dev libxslt-dev autoconf libc6-dev ncurses-dev libpq-dev
RUN apt-add-repository -y ppa:brightbox/ruby-ng
RUN apt-get -y update
RUN apt-get -y install ruby2.2 ruby2.2-dev 
RUN echo "gem: --no-ri --no-rdoc" > /root/.gemrc
RUN gem install bundler
RUN gem install passenger -v 5.0.7
RUN passenger-config install-agent
RUN passenger-config install-standalone-runtime
ENV PASSENGER_COMPILE_NATIVE_SUPPORT_BINARY=0 PASSENGER_DOWNLOAD_NATIVE_SUPPORT_BINARY=0