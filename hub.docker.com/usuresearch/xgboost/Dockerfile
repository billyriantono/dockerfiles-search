FROM debian:stretch-slim

LABEL maintainer="USU Software AG Katana"

RUN apt-get update && apt-get -yq dist-upgrade && \
    apt-get install -yq --no-install-recommends \
	ca-certificates \
	git \
	make \
	g++ && \
	apt-get clean && \
	rm -rf /var/lib/apt/lists/*
	
RUN cd /opt && \
    git clone --recursive https://github.com/dmlc/xgboost && \
    cd xgboost && \
    make -j4