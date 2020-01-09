# Base image ubuntu:19.04
FROM ubuntu:19.04

# Author
MAINTAINER Sebastian Hollizeck

# install the system requirement
RUN apt-get update && apt-get install -q --no-install-recommends -y wget g++ gcc make bzip2 git autoconf automake make g++ gcc build-essential zlib1g-dev libgsl0-dev curl git wget unzip tabix libncurses5-dev libbz2-dev liblzma-dev && rm -rf /var/lib/apt/lists/* && apt-get autoremove -y


WORKDIR /opt
# install vcflib
RUN wget --no-check-certificate https://github.com/vcflib/vcflib/releases/download/v1.0.1/vcflib-1.0.1-src.tar.gz \
 && tar -xvzf vcflib-1.0.1-src.tar.gz && mv vcflib-1.0.1-src vcflib && cd vcflib && make 

ENV PATH=/opt/vcflib/bin:$PATH


