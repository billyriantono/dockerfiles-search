FROM ubuntu:16.04

RUN apt-get update
RUN apt-get install -y make gcc g++ bison flex git libc6-dev gcc-multilib g++-multilib

WORKDIR /gbdk
COPY . .

RUN make
RUN make install