FROM ubuntu:xenial
MAINTAINER Yasuyuki YAMADA <yasuyuky@idein.jp>

RUN apt-get update
RUN apt-get install -y curl=7.* bzip2=1.* git=* g++ make
RUN git clone https://github.com/snap-stanford/snap
WORKDIR /snap/examples/node2vec
RUN make all
RUN cp node2vec /usr/local/bin
RUN mkdir /work
WORKDIR /work
