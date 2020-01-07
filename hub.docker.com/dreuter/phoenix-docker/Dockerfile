FROM ubuntu:14.04
MAINTAINER Daniel Reuter <daniel.robin.reuter@googlemail.com>

# Set the locale
RUN locale-gen en_US.UTF-8
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en
ENV LC_ALL en_US.UTF-8

# Avoids annoying warnings from debconf
RUN echo 'debconf debconf/frontend select Noninteractive' | debconf-set-selections

# Install curl
RUN apt-get update && apt-get -y install curl

# Install esl-erlang
RUN curl -sO https://packages.erlang-solutions.com/erlang-solutions_1.0_all.deb && dpkg -i erlang-solutions_1.0_all.deb && rm erlang-solutions_1.0_all.deb && apt-get update && apt-get -y install esl-erlang

# Install elixir
RUN apt-get -y install elixir

# Install npm and nodejs
# TODO: Don't just download a script and execute it, but rather put the contents of that script here
RUN curl -sL https://deb.nodesource.com/setup_5.x | sudo bash - && apt-get -y install nodejs build-essential

# Install posgres_client
RUN apt-get -y install postgresql-client

# Install hex
RUN yes | mix local.hex
