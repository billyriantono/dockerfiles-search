FROM ubuntu:14.04

MAINTAINER Joe Bullard <jbullard@reactive.co.jp>

RUN apt-get update \
    && apt-get install -y --no-install-recommends texlive make \
    && apt-get install -y --no-install-recommends latex-beamer texlive-bibtex-extra texlive-lang-cjk \
    && apt-get remove -y $(dpkg --get-selections | grep -o "texlive.*doc") \
    && apt-get clean \
    && rm -rf /var/cache/apt/lists/*

WORKDIR /project
