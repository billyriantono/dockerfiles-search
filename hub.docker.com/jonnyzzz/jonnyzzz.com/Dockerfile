FROM ubuntu:16.04

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update && \
    apt-get install -y apt-utils && \
    apt-get install -y curl wget mc vim git subversion ruby-full

#
# RUN  gpg --keyserver hkp://keys.gnupg.net --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3 \
#     curl -sSL https://get.rvm.io | bash -s stable --ruby
#

# that one seemed to fail on travis-ci.org
# RUN apt-get build-dep -y ruby-full

RUN apt-get update && \
    apt-get install -y autoconf gcc libc6-dev libssl-dev libmysql++-dev \
                       libsqlite3-dev make build-essential libssl-dev \
                       libreadline6-dev zlib1g-dev libyaml-dev

RUN apt-get update && \
    gem install bundler && \
    mkdir -p bundle/path && bundle config path /bundle/path

RUN curl -sL https://deb.nodesource.com/setup_10.x | bash - && \
    apt-get update && \
    apt-get install -y nodejs gcc g++ make

RUN apt-get update && \
    apt-get install -y build-essential checkinstall && \
    apt-get install -y libreadline-gplv2-dev libncursesw5-dev libssl-dev libsqlite3-dev tk-dev libgdbm-dev libc6-dev libbz2-dev && \
    apt-get install -y python python-pip && \
# crashes after update with v18    pip install --upgrade pip && \
    pip install Pygments

ADD build.sh Gem* README.md /srv/jekyll/
RUN /srv/jekyll/build.sh container || true

VOLUME srv/jekyll


