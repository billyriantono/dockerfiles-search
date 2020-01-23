FROM ubuntu:14.04

RUN apt-get update; apt-get install -y wget git-core curl zlib1g-dev build-essential libssl-dev libreadline-dev libyaml-dev libsqlite3-dev sqlite3 libxml2-dev libxslt1-dev libcurl4-openssl-dev python-software-properties libffi-dev
RUN wget http://ftp.ruby-lang.org/pub/ruby/2.3/ruby-2.3.1.tar.gz && \
    tar -xzvf ruby-2.3.1.tar.gz && \
    cd ruby-2.3.1 && \
    ./configure && \
    make && \
    make install && \
    cd ../ && \
    rm -rf ruby-2.3.1 ruby-2.3.1.tar.gz && \
    ruby -v

RUN echo 'deb http://download.virtualbox.org/virtualbox/debian trusty contrib non-free' > /etc/apt/sources.list.d/virtualbox.list && \
    wget -q http://download.virtualbox.org/virtualbox/debian/oracle_vbox.asc -O- | apt-key add - && \
    apt-get update && \
    apt-get install -y vagrant virtualbox-4.3 dkms
RUN apt-get clean
