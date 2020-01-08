FROM debian:jessie

MAINTAINER Manala <contact@elao.com>

RUN apt-get update \
    && DEBIAN_FRONTEND=noninteractive apt-get --no-install-recommends -y install \
      pandoc  \
      python-pip

RUN pip install MarkdownTools2

WORKDIR /srv

# Clean
RUN rm -rf * /var/lib/apt/lists/*
