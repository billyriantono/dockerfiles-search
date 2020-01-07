# Basic Unit Test container - based on Ubuntu 18.04
# Includes cmake, make and GCC.
#
# Copyright (c) 42 Technology Ltd
# This file is licensed under the MIT license

FROM ubuntu:18.04
LABEL com.42technology.unit-tests.version="1.2.0"
LABEL com.42technology.unit-tests.date="2019-05-01"
MAINTAINER Jonathan Pallant (jonathan.pallant@42technology.com)
RUN apt-get update && apt-get -y install gcc make cmake libc-dev lcov curl && rm -rf /var/lib/apt/lists/*
RUN mkdir /work
WORKDIR /work
CMD [ "bash" ]
