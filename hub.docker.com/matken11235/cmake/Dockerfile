#FROM ubuntu:16.04
FROM gcc:8

ENV DEBIAN_FRONTEND noninteractive


# Install cmake-3.11.3
RUN apt-get update -qq \
 && apt-get install -y -qq build-essential gcc wget \
 libcurl4-gnutls-dev \
 libtinfo5 \
 libstdc++6 \
 && wget -q https://cmake.org/files/v3.11/cmake-3.11.3.tar.gz \
 && tar -xzvf cmake-3.11.3.tar.gz \
 && cd cmake-3.11.3 \
 && ./bootstrap \
 && make -j4 \
 && make install

