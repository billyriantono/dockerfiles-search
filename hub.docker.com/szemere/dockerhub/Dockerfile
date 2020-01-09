FROM ubuntu:xenial as base

RUN apt update
RUN apt install -y wget

FROM base as devshell

RUN apt install -y curl
