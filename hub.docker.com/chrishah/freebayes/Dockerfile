FROM ubuntu:18.04

RUN apt-get update && apt-get -y upgrade && apt-get install -y build-essential wget zlib1g-dev libbz2-dev liblzma-dev git && \
        apt-get clean && apt-get purge && \
        rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

WORKDIR /usr/src
RUN git clone --recursive https://github.com/ekg/freebayes.git && \
	cd freebayes && \
	git reset --soft 8a0dbeeb49ec8449914b9698f8106fbd002b371c && \
	make && \
	make install
