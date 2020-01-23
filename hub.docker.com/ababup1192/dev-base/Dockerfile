FROM ubuntu:14.04
MAINTAINER ababup1192 ababup1192@gmail.com

# Install packages
RUN apt-get update && apt-get install -y software-properties-common
RUN add-apt-repository ppa:git-core/ppa && add-apt-repository ppa:pi-rho/dev
RUN apt-get update && apt-get install -y openssh-server zsh vim git curl autoconf tar wget \
  zlib1g-dev build-essential libssl-dev libreadline-dev libyaml-dev libsqlite3-dev \
  sqlite3 libxml2-dev libxslt1-dev libcurl4-openssl-dev \
  python-software-properties libffi-dev tmux

 # Install Java

 RUN \
   echo oracle-java8-installer shared/accepted-oracle-license-v1-1 select true | \
  debconf-set-selections
 RUN add-apt-repository ppa:webupd8team/java && apt-get update
 RUN apt-get install -y oracle-java8-installer && rm -rf /var/lib/apt/lists/*

 ENV JAVA_HOME /usr/lib/jvm/java-8-oracle

 WORKDIR /tmp
 RUN wget http://cx4a.org/pub/rsense/rsense-0.3.tar.bz2 && \
   bzip2 -dc rsense-0.3.tar.bz2 | tar xvf - && mv rsense-0.3 /usr/local/lib && \
   chmod +x /usr/local/lib/rsense-0.3/bin/rsense && rm rsense-0.3.tar.bz2
