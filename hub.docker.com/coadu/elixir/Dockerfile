FROM coadu/erlang

MAINTAINER Mads Flensted-Urech, Coadu.com

# TODO: find nicer way of enabling UTF-8?
RUN apt-get update && apt-get install --yes make locales

RUN echo "en_US.UTF-8 UTF-8" > /etc/locale.gen && \
    locale-gen

ENV LANG en_US.UTF-8

RUN git clone https://github.com/elixir-lang/elixir.git /usr/src/elixir && \
    cd /usr/src/elixir && \
    git checkout v1.0.2 && \
    make install
