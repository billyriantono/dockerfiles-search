FROM debian:jessie
MAINTAINER Beau Trepp <https://github.com/btrepp>
ENV DEBIAN_FRONTEND noninteractive
RUN apt-get clean && apt-get update && apt-get install -y  --no-install-recommends \
	git \
	build-essential \
	gcc \
	cmake \
	python \
	python-lxml \
	curl \
	check \
	pkg-config
WORKDIR /open62541
RUN curl -SLk https://github.com/acplt/open62541/archive/master.tar.gz \
	| tar xzC /open62541
WORKDIR /open62541/open62541-master/
RUN cmake -D BUILD_UNIT_TESTS=ON \
	  -DENABLE_AMALGAMATION=ON \
	.
RUN make
RUN make test
