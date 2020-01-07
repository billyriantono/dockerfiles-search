FROM ubuntu:16.04
MAINTAINER Vinicius Soares Batista <vbatista@gmail.com>

# Setup python and java and base system
ENV DEBIAN_FRONTEND noninteractive
ENV LANG=en_US.UTF-8

RUN apt-get update && apt-get install -q -y openjdk-8-jdk python3-pip maven ruby ruby-dev rubygems build-essential gettext-base
RUN gem install --no-ri --no-rdoc fpm