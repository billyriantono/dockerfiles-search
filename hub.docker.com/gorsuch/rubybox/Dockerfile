FROM ubuntu:trusty
MAINTAINER Michael Gorsuch <michael.gorsuch@gmail.com>

RUN apt-get update
RUN apt-get -y install curl build-essential git libssl-dev libreadline6 libreadline6-dev

# ruby-install
RUN curl https://github.com/postmodern/ruby-install/archive/v0.4.3.tar.gz -L -s | tar xvz
RUN cd ruby-install-0.4.3/ && make install
RUN ruby-install ruby 2.1.4

# env
ENV PATH /opt/rubies/ruby-2.1.4/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
ENV RUBY_ENGINE ruby
ENV GEM_ROOT /opt/rubies/ruby-2.1.4/lib/ruby/gems/2.1.0
ENV RUBY_ROOT /opt/rubies/ruby-2.1.4
ENV RUBY_VERSION 2.1.4

# bundler
RUN gem install bundler
