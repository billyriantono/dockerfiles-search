FROM ubuntu:16.04
MAINTAINER tsunoda

# 必要なパッケージの追加
RUN apt-get update && \
  apt-get upgrade -y && \
  apt-get clean && \
  apt-get install -y \
    curl && \
  rm -rf /var/cache/apt/archives/* && \
  rm -rf /var/lib/apt/lists/*
CMD /bin/bash
