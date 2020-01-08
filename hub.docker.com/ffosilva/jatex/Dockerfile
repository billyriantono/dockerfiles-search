FROM ubuntu:bionic

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update \
    && apt-get install -y make texlive-base texlive-fonts-extra texlive-xetex \
    && rm -rf /var/lib/apt/lists/*
