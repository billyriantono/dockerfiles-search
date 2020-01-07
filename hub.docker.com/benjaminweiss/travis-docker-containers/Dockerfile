FROM debian:9

RUN apt-get update \
  && apt-get install -y build-essential cmake ninja-build libboost-dev git python-pip \
  && pip install codecov
