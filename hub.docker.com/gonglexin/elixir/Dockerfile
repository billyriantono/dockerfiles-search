FROM gonglexin/elixir-ubuntu:18.04

LABEL maintainer="Lexin Gong <gonglexin@gmail.com>"

ENV ERLANG_VERSION=21.3.2-1 \
    ELIXIR_VERSION=1.8.1-2

WORKDIR /opt/build

RUN \
  wget https://mirrors.tuna.tsinghua.edu.cn/erlang-solutions/ubuntu/pool/esl-erlang_${ERLANG_VERSION}~ubuntu~bionic_amd64.deb && \
  wget https://mirrors.tuna.tsinghua.edu.cn/erlang-solutions/ubuntu/pool/elixir_${ELIXIR_VERSION}~ubuntu~bionic_amd64.deb && \
  dpkg -i esl-erlang_${ERLANG_VERSION}~ubuntu~bionic_amd64.deb && \
  apt-get -f -y install && \
  dpkg -i esl-erlang_${ERLANG_VERSION}~ubuntu~bionic_amd64.deb && \
  rm esl-erlang_${ERLANG_VERSION}~ubuntu~bionic_amd64.deb && \
  dpkg -i elixir_${ELIXIR_VERSION}~ubuntu~bionic_amd64.deb && \
  rm elixir_${ELIXIR_VERSION}~ubuntu~bionic_amd64.deb

CMD ["/bin/bash"]
