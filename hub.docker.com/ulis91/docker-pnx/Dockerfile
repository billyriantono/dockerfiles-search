FROM ubuntu:16.04

MAINTAINER  siguernstore@protonmail.com 

RUN apt-get update && apt-get install -y \
	build-essential libssl-dev libboost-all-dev git libdb5.3++-dev libminiupnpc-dev

RUN cd /root && git clone https://github.com/phantomxdev/phantomx.git

WORKDIR "/root"

VOLUME ["/root/.phantomx"]

RUN cd /root/phantomx/src/leveldb && chmod +x build_detect_platform && \
    cd .. && make -f makefile.unix && mv phantomxd /root/

ENTRYPOINT ["/root/phantomxd"]

