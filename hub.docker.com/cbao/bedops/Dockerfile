FROM ubuntu:16.04

RUN apt-get update && \
     apt-get upgrade -y && \
     apt-get install -y build-essential libc6-dev git

# bedops
RUN mkdir /tools
WORKDIR /tools

RUN git clone https://github.com/bedops/bedops.git && \
     cd bedops && \
     make && \
     make install && \
     cp bin/* /usr/local/bin

WORKDIR /
