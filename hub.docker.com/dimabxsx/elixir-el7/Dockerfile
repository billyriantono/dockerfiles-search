FROM centos:7.2.1511

ENV LANG="en_US.UTF-8"
ENV ELIXIR_VERSION="1.4.4"

RUN set -xe \
    && yum -y install epel-release \
    && yum -y install wget unzip git make \
    && wget https://packages.erlang-solutions.com/erlang-solutions-1.0-1.noarch.rpm \
    && rpm -Uvh erlang-solutions-1.0-1.noarch.rpm \
    && rm erlang-solutions-1.0-1.noarch.rpm \
    && yum -y install erlang \
    && wget https://github.com/elixir-lang/elixir/releases/download/v1.4.4/Precompiled.zip \
    && unzip -d /usr/local/ Precompiled.zip \
    && rm Precompiled.zip \
    && mix local.hex --force \
    && mix local.rebar --force
