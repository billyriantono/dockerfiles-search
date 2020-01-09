FROM shiguredo/erlang:erlang-19.0.2-ubuntu-14.04

MAINTAINER yamionp <yami@crimsondream.jp>

RUN apt-get update \
  && apt-get install -y \
         git \
  && apt-get clean \
  && rm -rf /var/cache/apt/archives/* /var/lib/apt/lists/*

