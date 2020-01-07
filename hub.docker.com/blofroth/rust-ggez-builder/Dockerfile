FROM rust:1.23

MAINTAINER Björn Löfroth <bjorn.lofroth@gmail.com>

# https://github.com/ggez/ggez/blob/master/docs/BuildingForEveryPlatform.md
RUN apt-get update \
    && apt-get install -y  \
         libasound2-dev \
         libsdl2-dev \
    && rm -rf /var/lib/apt/lists/*
