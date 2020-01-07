FROM ubuntu:18.04
LABEL maintainer="fabtesta@gmail.com" \
      version="1.0.0"

ENV DEBIAN_FRONTEND noninteractive

#up-to-date + encoding
RUN apt update && \
    apt upgrade -y && \
    apt install locales && \
    locale-gen en_US.UTF-8
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en
ENV LC_ALL en_US.UTF-8

#erlang + elixir
RUN apt install -y curl wget git make sudo gnupg gnupg1 gnupg2 && \
    wget https://packages.erlang-solutions.com/erlang-solutions_1.0_all.deb && \
    dpkg -i erlang-solutions_1.0_all.deb && \
    apt update && \
    rm erlang-solutions_1.0_all.deb && \
    apt install -y esl-erlang && \
    apt install -y elixir && \
    apt autoclean && apt --purge --yes autoremove

#phoenix mix archive
RUN mix local.hex --force && \
    mix archive.install hex --force phx_new 1.4.10

#nodejs lts
RUN curl -sL https://deb.nodesource.com/setup_10.x | sudo -E bash - && apt update && apt install -y inotify-tools nodejs

EXPOSE 4000

WORKDIR /code