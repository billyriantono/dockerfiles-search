#
# xptMiner Dockerfile
#
# https://github.com/mubarakzyanov/riecoin-miner
#

# Pull base image.
FROM ubuntu:xenial

# Install build tools and dependencies.
RUN apt-get update && apt-get install -y build-essential m4 openssl libssl-dev git libjson-c-dev libcurl4-openssl-dev wget libjansson-dev libprimesieve6-dev libgmp-dev

# Pull miner source code.
RUN git clone -b stratum https://github.com/dave-andersen/fastrie.git

# Compile miner sources.
RUN cd fastrie/xptMiner && LD_LIBRARY_PATH=/usr/local/lib  && make -j4

# Command to run miner.
CMD fastrie/xptMiner/xptminer -m -o $POOL_ADDRESS -u $POOL_USER -p $POOL_PASSWORD -t $THREAD_COUNT
