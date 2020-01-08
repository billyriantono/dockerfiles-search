FROM ubuntu:16.04

RUN apt-get update
RUN apt-get install -yq make make gcc g++ bison flex

ADD . /gbdk
WORKDIR /gbdk

RUN make install


