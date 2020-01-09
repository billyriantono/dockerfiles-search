FROM elixir:1.4.5
ARG DEBIAN_FRONTEND=noninteractive
ENV HOME=/opt/app/ TERM=xterm

RUN apt-get update && apt-get upgrade -y && apt-get install locales && locale-gen en_US.UTF-8

USER root

RUN mix local.hex --force \
 && mix local.rebar --force \
 && mix archive.install --force https://github.com/phoenixframework/archives/raw/master/phx_new.ez \
 && apt-get update \
 && apt-get install -y --assume-yes apt-utils \
 && apt-get install -y apt-transport-https \
 && apt-get install -y python \
 && apt-get install -y dialog \
 && apt-get install -y curl \
 && apt-get install -y make \
 && apt-get install -y sudo \
 && apt-get install -y g++ \
 && apt-get install -y gcc \
 && apt-get install -y libc6-dev \
 && apt-get install -y build-essential \
 && apt-get install -y bzip2 \
 && apt-get install -y libxml2 \
 && apt-get install -y libssl-dev \
 && apt-get install -y bash \
 && apt-get install -y gcc g++ libc-dev \
 && apt-get install -y erlang-dev \
 && apt-get install -y erlang-crypto \
 && apt-get install -y inotify-tools \
 && apt-get install -y imagemagick --fix-missing \
 && rm -rf /var/lib/apt/lists/*

RUN curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash - \
  && sudo apt-get install -y nodejs

WORKDIR $HOME
