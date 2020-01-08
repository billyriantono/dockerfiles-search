FROM debian:testing-slim

ENV LANG C.UTF-8

RUN apt-get update && apt-get install -y \
  par2 \
  lzop \
  lz4 \
  subversion \
  git \
  p7zip-full \
  && rm -rf /var/lib/apt/lists/*

WORKDIR /wrk
