#
From gankkank/ubuntu-ssh
MAINTAINER Jimmy Yang <gankkank@gmail.com>

RUN apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install -y \
  lsb-release psmisc \
  sudo vim git curl wget gzip

RUN \
  DEBIAN_FRONTEND=noninteractive apt-get install -y \
  build-essential autoconf software-properties-common python-pip \
  bison libssl-dev libyaml-dev libreadline6-dev zlib1g-dev libncurses5-dev libffi-dev libgdbm3 libgdbm-dev libsqlite3-dev

RUN \
  apt-add-repository ppa:brightbox/ruby-ng -y  && \
  apt-get update && \
  apt-get install -y ruby2.2 ruby2.2-dev

RUN \
  apt-get install -y \
  redis-tools

# For Development
RUN \
  gem install bundler

RUN \
  pip install awscli

# Clean
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

EXPOSE 80
