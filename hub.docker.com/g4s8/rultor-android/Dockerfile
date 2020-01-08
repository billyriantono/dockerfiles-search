FROM g4s8/ubuntu-base:latest
MAINTAINER Kirill <g4s8.public@gmail.com>
LABEL Description="Docker image for Rultor with Android support"

WORKDIR /tmp

ENV DEBIAN_FRONTEND=noninteractive

# UTF-8 locale
RUN locale-gen en_US en_US.UTF-8
RUN dpkg-reconfigure locales
ENV LC_ALL en_US.UTF-8
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US.UTF-8

# Basic Linux tools
RUN apt-get update
RUN apt-get install -y wget bcrypt curl
RUN apt-get install -y unzip zip
RUN apt-get install -y gnupg gnupg2
RUN apt-get install -y jq
RUN apt-get install -y bsdmainutils
RUN apt-get install -y libxml2-utils
RUN apt-get install -y build-essential
RUN apt-get install -y automake autoconf

# Git 2.0
RUN apt-get install -y software-properties-common python-software-properties
RUN add-apt-repository ppa:git-core/ppa
RUN apt-get update
RUN apt-get install -y git git-core

# SSH Daemon
RUN apt-get install -y ssh && \
  mkdir /var/run/sshd && \
  chmod 0755 /var/run/sshd

# Ruby (required for pdd)
RUN apt-get update && apt-get install -y ruby-dev libmagic-dev=1:5.14-2ubuntu3.3 \
  zlib1g-dev=1:1.2.8.dfsg-1ubuntu1
RUN gpg2 --keyserver hkp://keys.gnupg.net --recv-keys D39DC0E3
RUN curl -L https://get.rvm.io | bash -s stable
RUN /bin/bash -l -c "rvm requirements"
RUN /bin/bash -l -c "rvm install 2.3.3"
RUN /bin/bash -l -c "gem update && gem install --no-ri --no-rdoc nokogiri:1.6.7.2 bundler:1.11.2"

RUN rm -rf /tmp/*
RUN rm -rf /root/.ssh

ENTRYPOINT ["/bin/bash", "-l", "-c"]
