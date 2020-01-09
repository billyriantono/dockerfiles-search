FROM ubuntu:18.04

RUN apt-get update && apt-get -y upgrade && apt-get install -y build-essential vim git zlib1g-dev && \
	apt-get clean && apt-get purge && \
        rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

WORKDIR /usr/src

RUN git clone https://github.com/lh3/bwa.git && \
	cd bwa && \
	git reset --soft 20d0a13092aa4cb73230492b05f9697d5ef0b88e && \
	make && \
	ln -s $(pwd)/bwa /usr/bin
