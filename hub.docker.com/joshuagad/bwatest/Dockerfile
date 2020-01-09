FROM	alpine

LABEL	tool="bwa" version="0.7.17"

RUN	wget https://github.com/lh3/bwa/releases/download/v0.7.17/bwa-0.7.17.tar.bz2 \
&&	tar xf bwa-0.7.17.tar.bz2 \
&&	cd bwa-0.7.17 \
&&	apk add build-base zlib-dev \
&&	make -j \
&&	cp bwa /usr/local/bin/bwa \
&&	cd / \
&&	rm -rf bwa-0.7.17* \
&&	apk del build-base zlib-dev
