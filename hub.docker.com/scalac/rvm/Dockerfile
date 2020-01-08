FROM phusion/baseimage:latest

MAINTAINER Jakub Zubielik <jakub.zubielik@scalac.io>

RUN apt-get update && \
    apt-get upgrade -y -o Dpkg::Options::="--force-confold"

RUN apt-get install -y nodejs libmysqlclient-dev libpq-dev

RUN gpg --keyserver hkp://keys.gnupg.net --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3
RUN curl -sSL https://get.rvm.io | bash -s stable

RUN locale-gen en_US.UTF-8
ENV LC_ALL en_US.UTF-8
ENV LANG en_US.UTF-8

ENV RUBY_VERSION 2.3.0

RUN bash -l -c 'rvm requirements && \
    rvm install $RUBY_VERSION && \
    rvm use $RUBY_VERSION --default && \
    rvm rubygems current && \
    gem install bundler --no-doc --no-ri'

RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN mkdir /src
WORKDIR /src
ENTRYPOINT ["bash", "-l", "-c"]
CMD ["/sbin/my_init"]
