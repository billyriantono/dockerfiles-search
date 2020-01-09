FROM ubuntu:19.04
RUN apt-get update && apt-get install -y wget g++ make zlib1g-dev
RUN wget https://github.com/atks/vt/archive/0.5772.tar.gz && tar -xzf 0.5772.tar.gz && cd vt-0.5772 && make
