FROM ubuntu:trusty
MAINTAINER Alex McLain <alex@alexmclain.com>

# Set locale.
RUN locale-gen en_US.utf8
ENV LC_ALL en_US.utf8

# Install system packages.
RUN apt-get -qq update && \
    apt-get -y install git wget curl autoconf build-essential\
    libssl-dev libreadline-dev software-properties-common

# Install Erlang.
RUN wget https://packages.erlang-solutions.com/erlang-solutions_1.0_all.deb
RUN dpkg -i erlang-solutions_1.0_all.deb

# Install Elixir.
RUN apt-get -qq update && \
    apt-get -y install elixir
