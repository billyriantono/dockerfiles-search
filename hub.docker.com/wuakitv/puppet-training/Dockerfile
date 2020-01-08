FROM debian:8.6

MAINTAINER Carles Amigó, carles.amigo@rakuten.com

ENV PUPPET_VERSION 4.7.0
ENV LC_ALL en_US.UTF-8

RUN apt-get update && apt-get install -y \
    bundler \
    git \
    jq \
    locales \
    locales-all \
    lsb-release \
    net-tools \
    ssh \
    vim \
    && rm -rf /usr/share/doc/* && \
    rm -rf /usr/share/info/* && \
    rm -rf /tmp/* && \
    rm -rf /var/tmp/*

COPY Gemfile /
RUN bundle install

COPY examples/ /examples
WORKDIR /examples
ENV PATH /usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games
