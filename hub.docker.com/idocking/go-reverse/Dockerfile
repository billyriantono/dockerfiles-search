FROM golang:1.13.5

# install keystone && unicorn
RUN apt-get update && \
	apt-get -y install cmake && \
	mkdir -p /go/src/github.com/keystone-engine && \
	cd /go/src/github.com/keystone-engine && \
	git clone https://github.com/keystone-engine/keystone.git && \
	cd keystone/ && \
	mkdir build && \
	cd build && \
	../make-share.sh && \
	make && \
	make install && \
	mkdir -p /go/src/github.com/keystone-engine && \
	cd /go/src/github.com/keystone-engine && \
	git clone https://github.com/unicorn-engine/unicorn.git && \
	cd unicorn && \
	make && \
	make install

ENV LD_LIBRARY_PATH=/lib:/usr/lib:/usr/local/lib
